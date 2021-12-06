# Systemd Remote Logging (Centos 8) 

```
# Walkthrough 

# Install on main and secondary 
dnf install -y systemd-journal-remote 

# on main modify systemd-journal-remote 
# systemctl edit systemd-journal-remote 
[Service]
ExecStart=
ExecStart=/usr/lib/systemd/systemd-journal-remote --listen-http=-3 --output=/var/log/journal/remote/

```
