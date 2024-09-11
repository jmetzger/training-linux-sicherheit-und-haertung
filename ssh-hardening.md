# Harden ssh 

## sshd_config - root user

```
# best
PermitRootLogin no

# only possible with private/public key 
PermitRootLogin prohibit-password
```

## no forwarding please ! 

```
# only open this, if is needed 
AllowAgentForwarding no
AllowTcpForwarding no
#GatewayPorts no
X11Forwarding no 
#X11DisplayOffset 10
X11UseLocalhost yes
#PermitTTY yes
```

## Only specific users are allowed 

```
# only users in this group are allowed to login 
AllowGroups sshonly 
```
## ssh audit 

```
dnf install -y python3 python3-pip
pip3 install ssh-audit
ssh-audit ap1.t3isp.de 
```

## Hardening guide ssh-audit (RHEL 8)

  * https://www.ssh-audit.com/hardening_guides.html#rhel8

## Hardening guide ssh-audit (Ubuntu 22.04) 

  * https://www.ssh-audit.com/hardening_guides.html#ubuntu_24_04_lts

```
# Abweichend würden wir das mit ufw umsetzen (Punkt 6) 
# werden die Regeln geladen beim starten 
systemctl status ufw 

# läuft ufw
ufw status

# Throttling für ssh
# Setzen 
sudo ufw limit ssh
ufw enable 
```



## generic place for crypto policies .

```
/etc/crypto-policies 
```

## BSI - ssh 

  * https://www.bsi.bund.de/SharedDocs/Downloads/DE/BSI/Publikationen/TechnischeRichtlinien/TR02102/BSI-TR-02102-4.pdf?__blob=publicationFile&v=2
