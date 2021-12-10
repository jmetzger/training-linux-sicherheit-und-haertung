# Harden ssh 

## sshd_config 

```
# best
PermitRootLogin no

# only possible with private/public key 
PermitRootLogin prohibit-password
```
