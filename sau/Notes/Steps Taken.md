# Hack the Box - "Sau" - 10.10.11.224
# Enumeration
## Nmap
### Inital Scan
Command
```
nmap -A -vv -oA enum/nmap-initial 10.10.11.224
```

Output
```
PORT      STATE    SERVICE REASON         VERSION                                  
22/tcp    open     ssh     syn-ack ttl 63 OpenSSH 8.2p1 Ubuntu 4ubuntu0.7 (Ubuntu Linux; protocol 2.0)               
| ssh-hostkey:                                                                     
|   3072 aa:88:67:d7:13:3d:08:3a:8a:ce:9d:c4:dd:f3:e1:ed (RSA)                     
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDdY38bkvujLwIK0QnFT+VOKT9zjKiPbyHpE+cVhus9r/6I/uqPzLylknIEjMYOVbFbVd8rTGzbmXKJBdRK61WioiPlKjbqvhO/YTnlkIRXm4jxQgs+xB0l9WkQ0CdHoo/Xe3v7TBije+lqjQ2tvhUY
1LH8qBmPIywCbUvyvAGvK92wQpk6CIuHnz6IIIvuZdSklB02JzQGlJgeV54kWySeUKa9RoyapbIqruBqB13esE2/5VWyav0Oq5POjQWOWeiXA6yhIlJjl7NzTp/SFNGHVhkUMSVdA7rQJf10XCafS84IMv55DPSZxwVzt8TLsh2ULTpX8FELRVESVBMxV5
rMWLplIA5ScIEnEMUR9HImFVH1dzK+E8W20zZp+toLBO1Nz4/Q/9yLhJ4Et+jcjTdI1LMVeo3VZw3Tp7KHTPsIRnr8ml+3O86e0PK+qsFASDNgb3yU61FEDfA0GwPDa5QxLdknId0bsJeHdbmVUW3zax8EvR+pIraJfuibIEQxZyM=                
|   256 ec:2e:b1:05:87:2a:0c:7d:b1:49:87:64:95:dc:8a:21 (ECDSA)                    
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBEFMztyG0X2EUodqQ3reKn1PJNniZ4nfvqlM7XLxvF1OIzOphb7VEz4SCG6nXXNACQafGd6dIM/1Z8tp662Stbk=                          
|   256 b3:0c:47:fb:a2:f2:12:cc:ce:0b:58:82:0e:50:43:36 (ED25519)                  
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAICYYQRfQHc6ZlP/emxzvwNILdPPElXTjMCOGH6iejfmi 
80/tcp    filtered http    no-response
55555/tcp open     unknown syn-ack ttl 63                                          
| fingerprint-strings:                                                             
|   FourOhFourRequest:                                                             
|     HTTP/1.0 400 Bad Request                                                     
|     Content-Type: text/plain; charset=utf-8                                      
|     X-Content-Type-Options: nosniff                                              
|     Date: Sun, 26 Jan 2025 22:32:45 GMT                                          
|     Content-Length: 75                                                           
|     invalid basket name; the name does not match pattern: ^[wd-_\.]{1,250}$      
|   GenericLines, Help, Kerberos, LDAPSearchReq, LPDString, RTSPRequest, SSLSessionReq, TLSSessionReq, TerminalServerCookie:                                
|     HTTP/1.1 400 Bad Request                                                     
|     Content-Type: text/plain; charset=utf-8                                      
|     Connection: close                                                            
|     Request                                                                      
|   GetRequest:                                                                    
|     HTTP/1.0 302 Found                                                           
|     Content-Type: text/html; charset=utf-8                                       
|     Location: /web                                                               
|     Date: Sun, 26 Jan 2025 22:32:19 GMT                                          
|     Content-Length: 27                                                           
|     href="/web">Found</a>.                                                       
|   HTTPOptions:                                                                   
|     HTTP/1.0 200 OK                                                              
|     Allow: GET, OPTIONS                                                          
|     Date: Sun, 26 Jan 2025 22:32:19 GMT                                          
|_    Content-Length: 0
```

### Full Scan
Command
```
nmap -A -vv -p- -oA enum/nmap-full 10.10.11.224
```

Output
```
PORT      STATE    SERVICE REASON         VERSION                                  
22/tcp    open     ssh     syn-ack ttl 63 OpenSSH 8.2p1 Ubuntu 4ubuntu0.7 (Ubuntu Linux; protocol 2.0)               
| ssh-hostkey:                                                                     
|   3072 aa:88:67:d7:13:3d:08:3a:8a:ce:9d:c4:dd:f3:e1:ed (RSA)                     
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDdY38bkvujLwIK0QnFT+VOKT9zjKiPbyHpE+cVhus9r/6I/uqPzLylknIEjMYOVbFbVd8rTGzbmXKJBdRK61WioiPlKjbqvhO/YTnlkIRXm4jxQgs+xB0l9WkQ0CdHoo/Xe3v7TBije+lqjQ2tvhUY
1LH8qBmPIywCbUvyvAGvK92wQpk6CIuHnz6IIIvuZdSklB02JzQGlJgeV54kWySeUKa9RoyapbIqruBqB13esE2/5VWyav0Oq5POjQWOWeiXA6yhIlJjl7NzTp/SFNGHVhkUMSVdA7rQJf10XCafS84IMv55DPSZxwVzt8TLsh2ULTpX8FELRVESVBMxV5
rMWLplIA5ScIEnEMUR9HImFVH1dzK+E8W20zZp+toLBO1Nz4/Q/9yLhJ4Et+jcjTdI1LMVeo3VZw3Tp7KHTPsIRnr8ml+3O86e0PK+qsFASDNgb3yU61FEDfA0GwPDa5QxLdknId0bsJeHdbmVUW3zax8EvR+pIraJfuibIEQxZyM=                
|   256 ec:2e:b1:05:87:2a:0c:7d:b1:49:87:64:95:dc:8a:21 (ECDSA)                    
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBEFMztyG0X2EUodqQ3reKn1PJNniZ4nfvqlM7XLxvF1OIzOphb7VEz4SCG6nXXNACQafGd6dIM/1Z8tp662Stbk=                          
|   256 b3:0c:47:fb:a2:f2:12:cc:ce:0b:58:82:0e:50:43:36 (ED25519)                  
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAICYYQRfQHc6ZlP/emxzvwNILdPPElXTjMCOGH6iejfmi 
80/tcp    filtered http    no-response
55555/tcp open     unknown syn-ack ttl 63                                          
| fingerprint-strings:                                                             
|   FourOhFourRequest:                                                             
|     HTTP/1.0 400 Bad Request                                                     
|     Content-Type: text/plain; charset=utf-8                                      
|     X-Content-Type-Options: nosniff                                              
|     Date: Sun, 26 Jan 2025 22:32:45 GMT                                          
|     Content-Length: 75                                                           
|     invalid basket name; the name does not match pattern: ^[wd-_\.]{1,250}$      
|   GenericLines, Help, Kerberos, LDAPSearchReq, LPDString, RTSPRequest, SSLSessionReq, TLSSessionReq, TerminalServerCookie:                                
|     HTTP/1.1 400 Bad Request                                                     
|     Content-Type: text/plain; charset=utf-8                                      
|     Connection: close                                                            
|     Request                                                                      
|   GetRequest:                                                                    
|     HTTP/1.0 302 Found                                                           
|     Content-Type: text/html; charset=utf-8                                       
|     Location: /web                                                               
|     Date: Sun, 26 Jan 2025 22:32:19 GMT                                          
|     Content-Length: 27                                                           
|     href="/web">Found</a>.                                                       
|   HTTPOptions:                                                                   
|     HTTP/1.0 200 OK                                                              
|     Allow: GET, OPTIONS                                                          
|     Date: Sun, 26 Jan 2025 22:32:19 GMT                                          
|_    Content-Length: 0
```

## Port 55555
>![[Pasted image 20250126164203.png]]
 
---

# Vulnerabilities
### CVE-2023-27163 - SSRF
Using the CVE PoC by entr0pie(https://github.com/entr0pie/CVE-2023-27163) we are able to make a call to port 80 on the device that is filtered from outside the machine.
>![[Pasted image 20250127165758.png]]

We can now use the generated link to view the webpage on port 80, which is Maltrail v0.53.
>![[Pasted image 20250127165923.png]]

### Maltrail v0.53
Maltrail v0.53 is vulnerable to an Unauthenticated OS Command Injection(RCE).
Using the PoC scripted provided by spookier(https://github.com/spookier/Maltrail-v0.53-Exploit) we can make a request using the generated link from CVE-2023-27163 to exploit Maltrail.
>![[Pasted image 20250127170231.png]]

We gain access to the "puma" user on the machine.
>![[Pasted image 20250127170321.png]]

---

# Privilege Escalation

###SUDO permissions
The device gives permissions to run "sudo /usr/bin/systemctl status trail.service" with no password needed.
>![[Pasted image 20250127172427.png]]

After running the sudo command you can enter "!sh" in the pager to break out and open a root shell.
>![[Pasted image 20250127172553.png]]

---

# Loot
## User
Command
```
ifconfig;id;hostname;cat user.txt
```
>e592aaac5e07a312ac1ed5ab61cce0c7
![[Pasted image 20250127170357.png]]
## Root/Admin
Command
```
ifconfig;id;hostname;cat root.txt
```
>dea8fb769490ad9af522b462aed5bf97
![[Pasted image 20250127172707.png]]