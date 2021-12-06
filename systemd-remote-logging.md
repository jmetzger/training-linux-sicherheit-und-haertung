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

# aktiviert den socket 
systemctl enable systemd-journal-remote 
systemctl start systemd-journal-remote 

# on secondary adjust URL= in /etc/systemd/journal-upload.conf 
[Upload]
URL=http://192.168.33.10:19532

# Restart upload - daemon 
systemctl enable --now systemd-journal-upload 

```
