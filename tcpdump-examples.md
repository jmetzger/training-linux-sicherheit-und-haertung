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


## Refs: 

  * https://hackertarget.com/tcpdump-examples/
