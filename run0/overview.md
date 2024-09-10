# run0 

## not implemented in Rocky 9 and Ubuntu 22.04.

  * because starts with systemd version 256
  * systemctl --version show version
  * ubuntu 24.04 -> version 255
  * Rocky 9 -> version 252

## Disadvantage

  * Advanced config is a bit clumsy

## Advantage

  * More secure (runs under systemd-run under systemd-run0) - probably possible to implement 2-factor-authentication 
  * Create temporary service every in runs in own linux namespace
  * Does not fork processes like sudo, also better performance and security 

```
ls -la /usr/bin/sudo
# used SUID - bit (unprivileged can call it and it runs under root)
-rwsr-xr-x 1 root root 277936 Apr  8 16:50 /usr/bin/sudo
```


## Does it make sense 

  * If it is in Distro by default
  * If bug is fixed that you have enter passwort everytime for each run (not like in sudo)

## References 

  * https://linux-audit.com/systemd/run0-introduction-and-usage/
