# nftables 

## Generally ;o) 
```
# In IPtables, -> several chains and tables that are loaded by default.
iptables -L

In nftables, there are no default chains or tables.
```

## Ubuntu 20.04LTS -> 20.10 
```
Starting from Ubuntu 20.10 it will be the default system -> nftables 
```

## Walkthrough / migration to nftables 

### take care of current rules 
```
iptables-save > fwrules.txt
cat fwrules.txt
iptables-restore-translate -f fwrules.txt
iptables-restore-translate -f fwrules.txt > ruleset.nft
```

# now installing nftables 
```
apt install nftables
# important -> iptables will still work then 
# apt install iptables-nftables-compat # not needed for ubuntu 20.04 
systemctl enable --now nftables.service
```


# now load the rules to nft 
```
nft -f ruleset.nft
nft list ruleset
```

## Examples nft 
```

#review current configuration:
root@host [~]# nft list ruleset

#Add a new table, with family "inet" and table "filter":
root@host [~]# nft add table inet filter

#Add a new chain, to accept all inbound traffic:
root@host [~]# nft add chain inet filter input \{ type filter hook input priority 0 \; policy accept \}

#Add a new rule, to accept several TCP ports:
root@host [~]# nft add rule inet filter input tcp dport \{ ssh, telnet, https, http \} accept

#To show rule handles:
root@host [~]# nft --handle --numeric list chain family table chain

#To delete a rule:
root@host [~]# nft delete rule inet filter input handle 3

#To save the current configuration:
root@host [~]# nft list ruleset > /etc/nftables.conf

```

## Deleting rules / all rules 

```
# handle is an internal number that identifies a certain rule.

nft flush rule filter output
nft flush table filter

```


## Create a firewall config 

```
flush ruleset

# List all IPs and IP ranges of your traffic filtering proxy source.
define SAFE_TRAFFIC_IPS = {
    x.x.x.x/xx,
    x.x.x.x/xx,
    x.x.x.x,
    x.x.x.x
}

table inet firewall {

    chain inbound {

    	# By default, drop all traffic unless it meets a filter
    	# criteria specified by the rules that follow below.
        type filter hook input priority 0; policy drop;

        # Allow traffic from established and related packets.
        ct state established,related accept

        # Drop invalid packets.
        ct state invalid drop

        # Allow loopback traffic.
        iifname lo accept

        # Allow all ICMP and IGMP traffic, but enforce a rate limit
        # to help prevent some types of flood attacks.
        ip protocol icmp limit rate 4/second accept
        ip6 nexthdr ipv6-icmp limit rate 4/second accept
        ip protocol igmp limit rate 4/second accept

        # Allow SSH on port 22.
        tcp dport 22 accept

        # Allow HTTP(S).
        # -- From anywhere
        tcp dport { http, https } accept
        udp dport { http, https } accept
        # -- From approved IP ranges only
        # tcp dport { http, https } ip saddr $SAFE_TRAFFIC_IPS accept
        # udp dport { http, https } ip saddr $SAFE_TRAFFIC_IPS accept

        # Uncomment to allow incoming traffic on other ports.
        # -- Allow Jekyll dev traffic on port 4000.
        # tcp dport 4000 accept
        # -- Allow Hugo dev traffic on port 1313.
        # tcp dport 1313 accept

        # Uncomment to enable logging of denied inbound traffic
        # log prefix "[nftables] Inbound Denied: " flags all counter drop

    }

    chain forward {

        # Drop everything (assumes this device is not a router)
        type filter hook forward priority 0; policy drop;

        # Uncomment to enable logging of denied forwards
        # log prefix "[nftables] Forward Denied: " flags all counter drop

    }

    chain outbound {

        # Allow all outbound traffic
        type filter hook output priority 0; policy accept;

    }

}
```


### Ref: 

  * https://wiki.nftables.org/wiki-nftables/index.php/Simple_ruleset_for_a_server


## Some commands ;o

```
# add chain 
# lower priority first
nft add chain inet example_table example_chain { type filter hook input priority 10 \; policy drop \; }

## append at the end 
nft add rule inet my_table my_filter_chain tcp dport ssh accept

## add at the beginning
nft insert rule inet my_table my_filter_chain tcp dport http accept

```

## revert back to iptables 
```
‘firewallbackend‘ entry in /etc/firewalld/firewalld.conf back to ‘iptables‘,
```


## References 

  * https://www.liquidweb.com/kb/how-to-install-nftables-in-ubuntu/
  * 
