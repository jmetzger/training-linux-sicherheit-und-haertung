# Overview nftables (Ubuntu 22.04) 

## Prerequisites 

```
Disable firewalld and ufw if we you want to use nftables (by itself) 

systemctl stop firewalld 
```

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

## Gegenüberstellung iptables und nft (Befehle) 

```   
iptables -L  -> nft list table ip filter
iptables -L INPUT -> nft list chain ip filter INPUT

iptables -t nat -L PREROUTING nft list chain ip nat PREROUTING
```
