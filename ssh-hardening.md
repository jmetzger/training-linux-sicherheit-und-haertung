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
