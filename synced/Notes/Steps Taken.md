# Hack the Box - "Synced" - 10.129.228.37
# Enumeration
## Nmap
### Inital Scan
Command
```
nmap -A -vv -oA enum/nmap-initial 10.129.228.37
```

Output
```
PORT    STATE SERVICE REASON  VERSION
873/tcp open  rsync   syn-ack (protocol version 31)
```

### Full Scan
Command
```
nmap -A -vv -p- -oA enum/nmap-full 10.129.228.37
```

Output
```

```

---

# Vulnerabilities

Rsync is exposed.

Connect to target using rsync and list file shares.
```
rsync -ahvr rsync://10.129.228.37
```
![](../Attachments/Pasted%20image%2020230520204214.png)

Open File share.
```
rsync -ahvr rsync://10.129.228.37/public
```
![](../Attachments/Pasted%20image%2020230520204414.png)

---

# Loot

## Root/Admin
Command
```
cat flag.txt
```
>72eaf5344ebb84908ae543a719830519
![](../Attachments/Pasted%20image%2020230520204547.png)
