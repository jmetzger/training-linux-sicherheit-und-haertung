# Troubleshooting SELinux Centos 

## General saying 

```
## Assumption: Golden Rule of Centos/Redhat 

!!! If everything looks nice (permissions), but DOES NOT START 
it MIGHT BE selinux <-- !!! 
```
## Walkthrough with debugging 

### Step 1:

```
# /etc/httpd/conf/httpd.conf
# Ergänzen 
# Listen 83 

systemctl restart httpd 
```


## Step 2: Findout what got into the way, with smart tools

```
dnf whatprovides sealert 
dnf install -y setroubleshoot-server 
cd /var/log/audit

# this take a little while - grab some coffee 
sealert -a audit.log > report.txt
```

## Step 3: Debug and fix 

```
sealert -a /var/log/audit.log > report.txt
# Extract advice from file 
# find http_port_t
semanage port -l | grep 80
# an advice how to fix from report.txt
semanage port -a -t http_port_t -p tcp 83
semanage port -l | grep 83
systemctl start httpd
# now apache also listens on port 83
lsof -i
```

  * [Alternative way using sealert](selinux-sealert.md) 

