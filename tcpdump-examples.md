# Examples tcpdump 

## What interfaces are available for listening ? 

```
tcpdump -D 
# Eventually doublecheck with 
ip a

```

## -n / -nn (Disable hostname / port resolving) 

```
# I would always recommend to do so, because it saves performance 

# Do not do hostname lookups 
tcpdump -i ens3 -n

# Do not do hostname and port lookups 
tcpdump -i ens3 -nn 
```

## Exclude specific ports 

```
tcpdump ! -p stp -i eth0 
# more user friendly 
tcpdump -i eth0 not stp and not icmp
```

## Include ascii output 

```
# s0 show unlimited content 
# -A ASCII 
tcpdump -A -s0 port 80

```

## Only from and/or to a specific host 

```
# to or from host
tcpdump -i eth0 host 10.10.1.1

# To a specific host 
tcpdump -i eth0 dst 10.10.1.20
```

## Write to a pcap file 

```


```

## Only show GET requests 

```
# this show only all tcp packages 
tcpdump -i eth0 tcp 

# now let us filter specific ones -> 0x474554 -> is equivalent for GET as hex - numbers 
# https://www.torsten-horn.de/techdocs/ascii.htm
# tcp header has 20 bytes and maximum of 60 bytes, allowing for up to 40 bytes of options in the header.
tcpdump -s 0 -A -vv 'tcp[((tcp[12:1] & 0xf0) >> 2):4] = 0x47455420'

# Same goes for post - operations 
tcpdump -s 0 -A -vv 'tcp[((tcp[12:1] & 0xf0) >> 2):4] = 0x504f5354'

```



```
# Deeply explained here
https://security.stackexchange.com/questions/121011/wireshark-tcp-filter-tcptcp121-0xf0-24

```

## Extra http get/post urls 

```
# show linewise 
tcpdump -s 0 -v -n -l | egrep -i "POST /|GET /|Host:"




## Refs: 

  * https://hackertarget.com/tcpdump-examples/
