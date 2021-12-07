# Systemd Remote Logging (Centos 8) 

## Walkthrough 

```
# Walkthrough 

# Install on main and secondary 
dnf install -y systemd-journal-remote 

# on main modify systemd-journal-remote
# Find info by:
# systemctl cat systemd-journal-remote 
# systemctl edit systemd-journal-remote 
[Service]
ExecStart=
ExecStart=/usr/lib/systemd/systemd-journal-remote --listen-http=-3 --output=/var/log/journal/remote/

# aktiviert den socket 
systemctl enable systemd-journal-remote 
systemctl start systemd-journal-remote 

# on secondary adjust URL= in /etc/systemd/journal-upload.conf 
[Upload]
URL=http://192.168.33.10:19532

# Restart upload - daemon 
systemctl enable --now systemd-journal-upload 

# Result -> failed 
# systemctl status systemd-journal-upload 
# o http://192.168.33.10:19532/upload failed: Couldn't connect to server

```

```
# Troubelshooting on secondary 
# according to: 
```

  * [Troubleshooting a service on Centos (SELINUX)]()

## Assumption: Golden Rule of Centos/Redhat 
!!! If everything looks nice (permissions), but NOT START 
it MIGHT BE selinux <-- !!! 

## Check 1: Does service start in permissive mode of selinux  
sestatus
setenforce 0 


dnf whatprovides sealert 
dnf install -y setroubleshoot-server 
cd /var/log/audit
# this take a little while - grab some coffee 
sealert -a audit.log > report.txt

# now look into the report.txt.
# in most there are 2-3 solutions for you problem 


# on secondary 
logger -p local0.info testlogeintrag 
# show entries 
journalctl -e | grep testlogeintrag 

# on main 
# Show entries of log-directory of journal (systemd) 
journalctl -D /var/log/journal/remote 
```



