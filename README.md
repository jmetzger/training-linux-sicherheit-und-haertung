# Linux Sicherheit und Härtung

## Agenda

  1. sudo 
     * [sudo - not to !](sudo/sudo-not-to.md)
     * [sudo exercise](sudo/sudo-exercise.md)

  1. Wireshark / tcpdump / nmap
     * [Examples tcpdump](tcpdump-examples.md) 
     * [Example nmap](nmap.md) 
     
  1. Erweiterte Dateiattribute (xattr) 
     * [lsattr/chattr](lsattr-chattr.md)
   
  1. LSM-Modules (aka SELinux or apparmor) 
     * [Kernel Docs](https://www.kernel.org/doc/html/v5.15/admin-guide/LSM/index.html)
   
  1. SELinux 
     * [Debian Installation](selinux-debian.md)
     * [Important commands and files](selinux-commands.md)
     * [SELinux Walkthrough Rocky Linux](selinux.md) 
     * [SELinux Troubleshooting on Centos](selinux-troubleshooting-centos.md)
   
  1. apparmor 
     * [apparmor](apparmor.md) 
     * [apparmor walkthrough ubuntu](apparmor-walkthrough-ubuntu.md)
     * [apparmor and docker/kubernetes](apparmor-docker-kubernetes.md)
        
  1. Host Intrusion Detection 
     * [Overview](hids-overview.md) 
     * [Installation ossec on Ubuntu](ossec.md)
     * [Installation/Walkthrough ossec on Centos 8](ossec-centos8.md)
     * [AIDE on Ubuntu/Debian](aide.md)  
     * [Tripwire](tripwire.md) 
   
  1. Network Intrusion Detection 
     * [Overview](nids-overview.md) 
   
  1. Vulnerability / Vulnerability Scans 
     * [nikto](nikto.md) 
     * [apache - etags](apache-etags.md) 
     * [Lynis](lynis.md)
   
  1. Malware / Viren - Scans 
     * [maldet - lmd](maldet.md)
     * [clamav](clamav.md)
     
  1. Firewall 
     * [nftables](nftables-ubuntu-22-04.md)
     * [firewalld](firewalld.md)  
     
  1. IPSec 
     * [IPSec](ipsec.md)
     
  1. Documentation
     * [Telekom Compliance Guideline](https://github.com/jmetzger/TelekomSecurity.Compliance.Framework)
     * [Linux Security](http://schulung.t3isp.de/documents/linux-security.pdf)

## Backlog  

  1. Wireshark / tcpdump / nmap
     * [Examples tcpdump](tcpdump-examples.md) 
     * [Example nmap](nmap.md) 
     * [Detect nmap scans on server](https://nmap.org/book/nmap-defenses-detection.html)

  1. Network Intrusion Detection 
     * [Overview](nids-overview.md) 

  1. Host Intrusion Detection 
     * [Overview](hids-overview.md) 
     * [Installation ossec on Ubuntu](ossec.md)
     * [Installation/Walkthrough ossec on Centos 8](ossec-centos8.md)
     * [AIDE on Ubuntu/Debian](aide.md)  
  
  1. Logging 
     * [Overview Logging Systems](logging.md) 
     * [Remote logging with rsyslog](remote-rsyslog-logging.md)
     * [Remote logging with rsyslog and tls](rsyslog-remote-logging-ssl.md)
     * [Systemd Remote Logging](systemd-remote-logging.md)
  
  1. Local Security
     * [sgid - bit on files](sgid-bit.md)
     * [xattr - special permissions](xattr.md)
     * [cgroups on Redhat](cgroups-redhat.md) 
     * [Using otp-authentication](otp-auth.md)
  
  1. Disk Managemenet 
     * [Install partprobe/parted on Debian](partprobe-parted-debian.md)
     * [Verschlüsselung mit Cryptsetup](cryptsetup.md)
     * [Self Encryption Hard Disks (SED) vs. LUKS](sed-vs-luks.md)

  1. SELinux / appArmor  
     * [Install selinux on Debian](selinux-debian.md)
     * [SELinux including Walkthrough](selinux.md)
     * [SELinux - working with booleans](selinux-boolean.md)
     * [Troubleshoot with sealert on Centos/Redhat](selinux-sealert.md)
     * [SELinux Troubleshooting on Debian](selinux-troubleshooting-debian.md)
     * [SELinux Troubleshooting on Centos](selinux-troubleshooting-centos.md)

  1. Docker / Podman with Seccomp 
     * [Restricting Syscall in Docker/Podman](docker-seccomp.md)

  1. Attacks 
     * [Slow loris Attack - apache](/attacks/slow-loris-apache.md)
  
  1. Kernel Hardening 
     * [modules_disabled,unprivileged_bpf_disabled,kexec_load_disabled](kernel-hardening.md)
     * [Disable TCP timestamps](kernel-disable-tcp-timestamps.md)

  1. Vulnerability Scans 
     * [OpenVAS Installation on Ubuntu](openvas-ubuntu.md)
     * [OpenVAS Background](https://www.greenbone.net/en/product-comparison/)
     * [Nikto - commandline](nikto.md) 

  1. Securing Network Services 
     * [Securing Tomcat (Standalone)](securing-tomcat.md) 
     * [Securing apache (Centos 8)](apache.md)
     * [SSL with letsencrypt apache (Centos 8)](apache-letsencrypt-ssl.md)
     * [SSL Testing / Config Hints](apache-testing-config-hints.md) 
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
     * [Kill Chain](kill-chain.md) 
   
  1. Server Automation 
     * [gitops by example (Ansible)](gitops-by-example.md) 

  1. Starting 
     * [How to begin with security/securing](howto-begin.md)

  1. Documentation 
     
 

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
 
