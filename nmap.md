# nmap - examples 

```
Server 1:
nmap -p 80 --script=http-enum.nse targetip 

Server 2: 
tcpdump -nn port 80 | grep "GET /" 
```
