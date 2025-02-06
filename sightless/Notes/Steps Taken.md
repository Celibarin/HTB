# Hack the Box - "Sightless" - 10.129.18.227
# Enumeration
## Nmap
### Inital Scan
Command
```
nmap -A -vv -oA enum/nmap-initial 10.10.10.
```

Output
>![[Pasted image 20240909093607.png]]

### Full Scan
Command
```
nmap -A -vv -p- -oA enum/nmap-full 10.10.10.
```

Output


## Port 80

>![[Pasted image 20240909093849.png]]

SQLPad page found on Domain
>![[Pasted image 20240909100746.png]]
>![[Pasted image 20240909100806.png]]

Found the version of SQLPad from the About link
>![[Pasted image 20240909100917.png]]
 
---

# Vulnerabilities

SQLPad 6.10.0 is vulnerable to SSTI}(CVE-2022-0944)
Creating a new connection and tested all the fields. Found "Database Key Path" returns file name
>![[Pasted image 20240909105005.png]]

Tested for SSTI for that field and verified it worked.
>![[Pasted image 20240909105046.png]]

Using SSTImap I was able to inject a reverse shell.
>![[Pasted image 20240909113333.png]]

>![[Pasted image 20240909113357.png]]
>![[Pasted image 20240909113426.png]]

Python does not exist on the machine so I used Perl to get a better shell.
```
perl -e 'system("bash -i");'
```
>![[Pasted image 20240909113543.png]]


---

# Privilege Escalation

### User
I was able to find a password for the user in the shadow file.
>![[Pasted image 20240909153159.png]]

Brute for of the password was successful:
>![[Pasted image 20240909153315.png]]
>`micahel:insaneclownposse`

Was successfully able to use the password to login via SSH.
>![[Pasted image 20240909153426.png]]

---

# Loot
## User
Command
```
ifconfig;id;hostname;cat user.txt
```
>![[Pasted image 20240909153527.png]]
>98c17d4dad54ec1544482fbffec2e74f

## Root/Admin
Command
```
ifconfig;id;hostname;cat root.txt
```
>
