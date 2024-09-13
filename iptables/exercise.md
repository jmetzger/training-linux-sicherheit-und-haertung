# Exercise (Ubuntu) 

## Walkthrough 

```
# ufw deaktivieren 
ufw disable
systemctl stop ufw
systemctl disable ufw 
```

```
# Erlauben für eingehenden Traffik 
iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
iptables -A INPUT -p tcp --dport 22 -j ACCEPT


# Policy 
iptables -P INPUT DROP
iptables -L

# Wir wollen ein Log eintrag machen
iptables -A INPUT -p tcp --dport 22  -j LOG
# Oh doch nicht falsche Stelle
iptables -L --line-numbers
ä Delete Line 3 -> Log line 
iptables -D INPUT 3 

# Now insert in line 2 / as new line 2 
iptables -I INPUT 2 -p tcp --dport 22  -j LOG --log-prefix "Jochen Meldung:"
iptables -L --line-numbers



```

```
iptables -F
```

```
# persistent auch nach Booten
apt install iptables-persistent
# Speichert automatisch die bestehenden Regeln in /etc/iptables/rules.v4

# Oder man schreibt sie direkt dort ein mit
iptables-save > /etc/iptables/rules.v4


```
