# Overview nftables (Ubuntu 22.04) 

## Prerequisites 

```
Disable firewalld and ufw if we you want to use nftables (by itself) 

systemctl stop firewalld
systemctl disable firewalld
```

## Schaubild 

  * https://www.teldat.com/blog/wp-content/uploads/2020/11/figure_05.png

## Hierarchie-Ebenen 

### Ebene 1: Ruleset 

```
# quasi das Gehäuse 
nft list ruleset 

# Leer ? 
# Per default ist noch nichts hinterlegt. 

# Config wie in iptables INPUT, OUTPUT, FORWARD 
# System hat einen Vorschlag 
# Dieser findet sich in
# Das ist auch gleichzeitig die Konfigurationsdatei 
# /etc/nftables.conf 
# Beim Starten werden diese Regeln geladen. 
# Und zwar mit folgendem Dienst 
systemctl status nftables 
systemctl start nftables
systemctl status nftables
nft list ruleset
```

### Ebene 2: Table 

### Ebene 3: Chain 


### Ebene 4: Rule 


## Gegenüberstellung iptables und nft (Befehle) 

```   
iptables -L  -> nft list table ip filter
iptables -L INPUT -> nft list chain ip filter INPUT

iptables -t nat -L PREROUTING nft list chain ip nat PREROUTING
```

## Beispiel 1:

 
```
flush ruleset

table inet firewall {
                                                                                 
    chain inbound_ipv4 {
        # accepting ping (icmp-echo-request) for diagnostic purposes.
        # However, it also lets probes discover this host is alive.
        # This sample accepts them within a certain rate limit:
        #
        # icmp type echo-request limit rate 5/second accept      
    }

    chain inbound_ipv6 {                                                         
        # accept neighbour discovery otherwise connectivity breaks
        #
        icmpv6 type { nd-neighbor-solicit, nd-router-advert, nd-neighbor-advert } accept
                                                                                 
        # accepting ping (icmpv6-echo-request) for diagnostic purposes.
        # However, it also lets probes discover this host is alive.
        # This sample accepts them within a certain rate limit:
        #
        # icmpv6 type echo-request limit rate 5/second accept
    }

    chain inbound {                                                              

        # By default, drop all traffic unless it meets a filter
        # criteria specified by the rules that follow below.
        type filter hook input priority 0; policy drop;

        # Allow traffic from established and related packets, drop invalid
        ct state vmap { established : accept, related : accept, invalid : drop } 

        # Allow loopback traffic.
        iifname lo accept

        # Jump to chain according to layer 3 protocol using a verdict map
        meta protocol vmap { ip : jump inbound_ipv4, ip6 : jump inbound_ipv6 }

        # Allow SSH on port TCP/22 and allow HTTP(S) TCP/80 and TCP/443
        # for IPv4 and IPv6.
        tcp dport { 22, 80, 443} accept

        # Uncomment to enable logging of denied inbound traffic
        # log prefix "[nftables] Inbound Denied: " counter drop
    }                                                                            
                                                                                 
    chain forward {                                                              
        # Drop everything (assumes this device is not a router)                  
        type filter hook forward priority 0; policy drop;                        
    }                                                                            
                                                                                 
    # no need to define output chain, default policy is accept if undefined.
}
```



## Documentation 

  * https://wiki.nftables.org/wiki-nftables/index.php/Quick_reference-nftables_in_10_minutes
