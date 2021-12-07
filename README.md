# Linux Security and Hardening 

## Agenda 

  1. Wireshark / tcpdump / nmap
     * [Examples tcpdump](tcpdump-examples.md) 
     * [Example nmap](nmap.md) 
     * [Detect nmap scans on server](https://nmap.org/book/nmap-defenses-detection.html)

  1. Host Intrusion Detection 
     * [Installation ossec on Ubuntu](ossec.md)
     * [AIDE on Ubuntu/Debian](aide.md)  
  
  1. Logging 
     * [Overview Logging Systems](logging.md) 
     * [Remote logging with rsyslog](rsyslog-remote-logging.md)
     * [Remote logging with rsyslog and tls](rsyslog-remote-logging-ssl.md)
  
  1. Disk Managemenet 
     * [Install partprobe/parted on Debian](partprobe-parted-debian.md)
     * [Verschlüsselung mit Cryptsetup](cryptsetup.md)
     * [Self Encryption Hard Disks (SED) vs. LUKS](sed-vs-luks.md)

  1. SELinux / appArmor  
     * [Install selinux on Debian](selinux-debian.md)
     * [SELinux including Walkthrough](selinux.md)
     * [SELinux Troubleshooting on Debian](selinux-troubleshooting-debian.md)
     * [SELinux Troubleshooting on Centos](selinux-troubleshooting-centos.md)

  1. Docker / Seccomp 
     * [Restricting Syscall in Docker](docker-seccomp.md)

  1. Firewall 
     * [nftables](nftables.md)
     * [firewalld](firewalld.md)
  
  1. Kernel Hardening 
     * [modules_disabled,unprivileged_bpf_disabled,kexec_load_disabled](kernel-hardening.md)
     * [Disable TCP timestamps](kernel-disable-tcp-timestamps.md)

  1. Vulnerability Scans 
     * [OpenVAS Installation on Ubuntu](openvas-ubuntu.md)
     * [OpenVAS Background](https://www.greenbone.net/en/product-comparison/)
     * [Nikto - commandline](nikto.md) 

  1. Securing Network Services 
     * [Securing Tomcat (Standalone)](securing-tomcat.md) 
     * [SSH](securing-ssh.md) 
     * [ssh-ca](ssh-ca.md)

  1. Virtualization 
     *  [Security Docker](security-docker.md)

  1. Hacking 
     * [Install Metasploitable 2](metasploitable2.md)
     * [Install Metasploit on Digitalocean - Version 1 (Ubuntu)](https://secprentice.medium.com/how-to-build-inexpensive-red-team-infrastructure-dfb6af0fe15d)
     * [Install Metasploit on Digitalocean - Version 2 (Ubuntu)](https://webtips4u.com/guides/linux/learn-how-to-install-metasploit-framework-on-ubuntu-18-04-16-04/)
     * [ReverseShell](reverse-shell.md)
     * [Hacking I - ShellShock (unprivileged permissions)](hacking.md)
     * [Hacking II - privilege escalation](hacking-privilege-escalation.md)

  1. Basics 
     * [Type of Attackers](attackers.md) 
     * [Basic Principles](basic-principles-security.md) 
   
  1. Server Automation 
     * [gitops by example (Ansible)](gitops-by-example.md) 

  1. Documentation 
      * [Telekom Compliance Guideline](https://github.com/jmetzger/TelekomSecurity.Compliance.Framework)
      * [Linux Security](http://schulung.t3isp.de/documents/linux-security.pdf)
 

## Change language on Ubuntu 

```
dpkg-reconfigure locales 
# see locales that are current configured
locale 
# place where it is configured 
/etc/default/locale 

# After that relogin or do 
# su student 
locale 
```

## tcpdump 

  * https://danielmiessler.com/study/tcpdump/
  
## Patching of packages (e.g.) 
 
  * Ubuntu will patch packages when CVE's occur 
  * https://ubuntu.com/security/CVE-2020-11984

## Search - Engine IoT 

  * https://www.shodan.io/
  
## Secure grub with password (not at boot but for changes and subentries 

```
#  Create password 
#  e.g. password 
grub-mkpasswd-pbkdf2

# /etc/grub.d/01_password 
#!/bin/sh
set -e 

cat << EOF 
set superusers='grub'
password_pbkdf2 grub grub.pbkpdf2.sha512.....
EOF

##
chmod a+x /etc/grub.d/01_password 

## Datei 10_linux 
## Variable CLASS
## at then 
## 
CLASS="--class gnu-linux ..... --unrestricted" 

update-grub 

```
## rsyslog 

### Basics 

```
# Hyphen before filename : -/..... 
# is for syncing but enabled by default since 
https://serverfault.com/questions/463170/what-does-filepath-action-mean-in-rsyslog-configuration
## it is set on by default anyways 
# You may prefix each entry with the minus “-‘’ sign to omit syncing the file after every logging.
```

### Bug on ubuntu kern.* logs to user.* 

```
logger -p kern.debug "Testmessage"
# that one logs to user.* 
```
 
### Walkthrough remote logging ubuntu

```
/etc/rsyslog.conf.d/99_remote.conf

# Provides UDP syslog reception
$ModLoad imudp 
$UDPServerRun 514
# Provides TCP syslog reception
$ModLoad imtcp 
$InputTCPServerRun 514

3. Then restart rsyslog:
# systemctl restart rsyslog
4. and generate a test message:
    
$ logger -p local0.info 'test logging'
Confirm the test message was written to the log:
# tail -n 100 /var/log/messages
```

```
# On secondary.example.com
#/etc/rsyslog.d/99-forward.conf 

# Provides UDP forwarding
*.*   @192.168.1.10
# Provides TCP forwarding
*.*   @@192.168.1.10
# systemctl restart  rsyslog
#Test by using the logger utility on the client, secondary.example.com, and view the message on the server, main. example.com.
#The configuration from this exercise will be used in the next exercise. Please keep the changes.

```
 
## systemd-journald -> remote logging 

```
# Step 1
on both machines:
main and secondary
apt install systemd-journal-remote

# Step 1a
cp -a /lib/systemd/system/systemd-journal-remote.service /etc/systemd/systemd-journal-remote
# Change line with ExecStart -> param https to http 

# Step 2 
# on secondary 
/etc/systemd/journal-upload.cnf
[Upload]
URL=http://192.168.56.103:19532

# Step 2a 
# Start service 
systemctl start systemd-journal-upload
systemctl status systemd-journal-upload

# Testing 
# on main 
journalctl -f -D /var/log/journal/remote 
# on seocndary
logger 'test logging"

```

## setroubleshoot -> alert 

```
### as of 2021-11-21
### Only available on Centos/Redhat/Rocky.. but not Ubuntu/Debian !! 
# install setroubleshoot 
yum install troubleshoot 
sealert -a /var/log/audit/audit.log
```

## Create a module and load it 

```
ausearch -c 'httpd' --raw | audit2allow -M my-httpd
semodule -X 300 -i my-httpd.pp
```


  
