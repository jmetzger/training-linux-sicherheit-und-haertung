# Overview nftables (Ubuntu 22.04) 

## Prerequisites 

```
Disable firewalld and ufw if we you want to use nftables (by itself) 

systemctl stop firewalld 
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

## Ebene 2: Table 

## Ebene 3: Chain 


## Ebene 4: Rule 


## Gegenüberstellung iptables und nft (Befehle) 

```   
iptables -L  -> nft list table ip filter
iptables -L INPUT -> nft list chain ip filter INPUT

iptables -t nat -L PREROUTING nft list chain ip nat PREROUTING
```

## Beispiel 2:




## Documentation 

  * https://wiki.nftables.org/wiki-nftables/index.php/Quick_reference-nftables_in_10_minutes
