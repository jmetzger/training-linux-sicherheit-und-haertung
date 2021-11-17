# nmap - examples 

## Example 1 

```
Server 1:
nmap -p 80 --script=http-enum.nse targetip 

Server 2: 
tcpdump -nn port 80 | grep "GET /" 
```

## Ref:

  * http://schulung.t3isp.de/documents/linux-security.pdf
