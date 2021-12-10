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

## Only specific users are allowd 

```
# only users in this group are allowed to login 
AllowGroups sshonly 
```
## ssh audit 

```
dnf install python3
pip3 install ssh-audit
ssh-audit ap1.t3isp.de 
```

## Hardening guide ssh-audit 

  * https://www.ssh-audit.com/hardening_guides.html#rhel8

## generic place for crypto policies .

```
/etc/crypto-policies 
```

## BSI - ssh 

  * https://www.bsi.bund.de/SharedDocs/Downloads/DE/BSI/Publikationen/TechnischeRichtlinien/TR02102/BSI-TR-02102-4.pdf?__blob=publicationFile&v=2
