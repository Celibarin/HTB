# Initial Scan
```

```
---
# Full Scan
```
    PORT STATE SERVICE REASON VERSION  
80/tcp open http syn-ack ttl 127 Microsoft IIS httpd 8.5  
| http-methods:  
| Supported Methods: OPTIONS TRACE GET HEAD POST  
|\_ Potentially risky methods: TRACE  
|\_http-server-header: Microsoft-IIS/8.5  
|\_http-title: IIS Windows Server  
135/tcp open msrpc syn-ack ttl 127 Microsoft Windows RPC  
139/tcp open netbios-ssn syn-ack ttl 127 Microsoft Windows netbios-ssn  
445/tcp open microsoft-ds syn-ack ttl 127 Microsoft Windows Server 2008 R2 - 2012 microsoft-ds  
1521/tcp open oracle-tns syn-ack ttl 127 Oracle TNS listener 11.2.0.2.0 (unauthorized)  
49152/tcp open msrpc syn-ack ttl 127 Microsoft Windows RPC  
49153/tcp open msrpc syn-ack ttl 127 Microsoft Windows RPC  
49154/tcp open msrpc syn-ack ttl 127 Microsoft Windows RPC  
49155/tcp open msrpc syn-ack ttl 127 Microsoft Windows RPC  
49159/tcp open oracle-tns syn-ack ttl 127 Oracle TNS listener (requires service name)  
49160/tcp open msrpc syn-ack ttl 127 Microsoft Windows RPC  
49161/tcp open msrpc syn-ack ttl 127 Microsoft Windows RPC  
No exact OS matches for host (If you know what OS is running on it, see [https://nmap.org/submit/](https://nmap.org/submit/) ).  
TCP/IP fingerprint:  
OS:SCAN(V=7.91%E=4%D=5/18%OT=80%CT=1%CU=38145%PV=Y%DS=2%DC=T%G=Y%TM=60A44EB  
OS:A%P=x86\_64-pc-linux-gnu)SEQ(SP=106%GCD=1%ISR=107%TI=RD%TS=4)SEQ(SP=106%G  
OS:CD=2%ISR=107%TI=RD%CI=RD%TS=6)SEQ(SP=106%GCD=1%ISR=107%TS=7)OPS(O1=M54DN  
OS:W8ST11%O2=M54DNW8ST11%O3=M54DNW8NNT11%O4=M54DNW8ST11%O5=M54DNW8ST11%O6=M  
OS:54DST11)WIN(W1=2000%W2=2000%W3=2000%W4=2000%W5=2000%W6=2000)ECN(R=Y%DF=Y  
OS:%T=80%W=2000%O=M54DNW8NNS%CC=Y%Q=)T1(R=Y%DF=Y%T=80%S=O%A=S+%F=AS%RD=0%Q=  
OS:)T2(R=Y%DF=Y%T=80%W=0%S=Z%A=S%F=AR%O=%RD=0%Q=)T3(R=Y%DF=Y%T=80%W=0%S=Z%A  
OS:=O%F=AR%O=%RD=0%Q=)T4(R=Y%DF=Y%T=80%W=0%S=A%A=O%F=R%O=%RD=0%Q=)T5(R=Y%DF  
OS:=Y%T=80%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=80%W=0%S=A%A=O%F=R%O=  
OS:%RD=0%Q=)T7(R=Y%DF=Y%T=80%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%T=80%  
OS:IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=80%CD=Z)  
  
Uptime guess: 0.012 days (since Tue May 18 19:15:50 2021)  
Network Distance: 2 hops  
TCP Sequence Prediction: Difficulty=263 (Good luck!)  
IP ID Sequence Generation: Randomized  
Service Info: OSs: Windows, Windows Server 2008 R2 - 2012; CPE: cpe:/o:microsoft:windows  
  
Host script results:  
|\_clock-skew: mean: 1m53s, deviation: 0s, median: 1m53s  
| p2p-conficker:  
| Checking for Conficker.C or higher...  
| Check 1 (port 21337/tcp): CLEAN (Couldn't connect)  
| Check 2 (port 52707/tcp): CLEAN (Couldn't connect)  
| Check 3 (port 38458/udp): CLEAN (Failed to receive data)  
| Check 4 (port 64791/udp): CLEAN (Timeout)  
|\_ 0/4 checks are positive: Host is CLEAN or ports are blocked  
| smb-security-mode:  
| authentication\_level: user  
| challenge\_response: supported  
|\_ message\_signing: supported  
| smb2-security-mode:  
| 2.02:  
|\_ Message signing enabled but not required  
| smb2-time:  
| date: 2021-05-18T23:35:03  
|\_ start\_date: 2021-05-18T23:30:52
```
---