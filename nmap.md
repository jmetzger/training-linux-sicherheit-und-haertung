# nmap - examples 

## Example 1 

```
# including additional information 
nmap -A main.training.local 
```

## Example 1a

```
nmap -A -F -T4 192.168.56.102
```

## Example 2

```
# ping target system 
nmap -sP main
```


## Example 3 

```
Server 1:
nmap -p 80 --script=http-enum.nse targetip 

Server 2: 
tcpdump -nn port 80 | grep "GET /" 
```

## Ref:

  * http://schulung.t3isp.de/documents/linux-security.pdf
