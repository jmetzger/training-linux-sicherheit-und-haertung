# Logging 

  * syslog 
  * auditd 
  * netfilter (iptables) 
  * systemd-journald 

# journalctl 

```
journalctl -u httpd.service  

# everything with pid = process id = 1 
journalctl _PID=1
