# Cgroups (Redhat)

## Why ? 

  * Allows restriction to resources 
 
## What are the most important categories 

  * The number of CPU shares per process.
  * The limits on memory per process.
  * Block Device I/O per process.
  * Mark network packets to be identified as the same type 
    * another application can use that to enforce traffic rules  

## What else (Redhat) ? 

  * There are 2 versions, v1 and v2
  * Although RHEL 8 allows v2, it is disabled 
  * All applications currently use v1  

## Install cgroup tools (Redhat) 

  * This way of working with cgroups is deprecated in RHEL 8 

```
dnf install -y libcgroup libcgroup-tools
```

## Show informations about cgroups 

```
cat /proc/cgroups
ps xawf -eo pid,user,cgroup,args
systemd-cgls
systemd-cgtop
```

## Walkthrough.  

```
# Step 1: Create a new cgroup 
cgcreate -g cpu,memory,blkio,devices,freezer:/resourcebox

# Step 2: Restrict zu 10% per CPU-core 
cgset -r cpu.cfs_period_us=100000 \
 -r cpu.cfs_quota_us=$[ 10000 * $(getconf _NPROCESSORS_ONLN) ] \
 resourcebox

# Step 3: Restrict memory in cgroup to 256MB
cgset -r memory.limit_in_bytes=256M resourcebox

# Step 4: Restrict access to 1 MB/s 
for dev in 253:0 252:0 252:16 8:0 8:16 1:0; do
 cgset -r blkio.throttle.read_bps_device="${dev} 1048576" resourcebox
 cgset -r blkio.throttle.write_bps_device="${dev} 1048576" resourcebox
done

# Step 5: no access to dev-files please 
cgset -r devices.deny=a resourcebox

# Step 6: allow access to console, null, zero rand and urandom 
for d in "c 5:1" "c 1:3" "c 1:5" "c 1:8" "c 1:9"; do
 cgset -r devices.allow="$d rw" resourcebox
done

# Step 7: execute program in cgroup (bash as an example) 
cgexec -g cpu,memory,blkio,devices,freezer:/resourcebox \
 prlimit --nofile=256 --nproc=512 --locks=32 /bin/bash

# Step 8: delete cgroup 
cgdelete -g cpu,memory,blkio,devices,freezer:/resourcebox

```

## Restrict system resources with systemd-run 

```
# Start stress test twice 
systemd-run stress -c 3
systemd-run stress -c 3


systemctl show run-r<UUID>.service
# default is 3600
systemctl set-property run-r<UUID>.service CPUShares=100
systemctl set-property run-r<UUID>.service CPUQuota=100

```

systemd Sicherheit
• http://0pointer.de/blog/projects/security.html [http://0pointer.de/blog/projects/security.html]
Einfache Direktiven
• Units unter anderer uid/gid laufen lassen
• Zugriff auf Verzeichnisse beschränken
• Prozesslimits setzen
$EDITOR /etc/systemd/system/simplehttp.service
[Unit]
Description=HTTP Server
[Service]
Type=simple
Restart=on-failure
#User=karl
#Group=users
#WorkingDirectory=/usr/share/doc
#PrivateTmp=yes
#ReadOnlyDirectories=/var
#InaccessibleDirectories=/home /usr/share/doc
#LimitNPROC=1 #darf nicht forken
#LimitFSIZE=0 #darf keine Files schreiben
ExecStart=/bin/python -m SimpleHTTPServer 8000

## References (Redhat) 

  * https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/resource_management_guide/chap-using_libcgroup_tools
  * https://www.redhat.com/sysadmin/cgroups-part-one
