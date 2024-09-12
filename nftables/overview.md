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

## revert back to iptables 
```
‘firewallbackend‘ entry in /etc/firewalld/firewalld.conf back to ‘iptables‘,
```


## References 

https://www.liquidweb.com/kb/how-to-install-nftables-in-ubuntu/
