# Notes for Linux Foundation Training 02/2021 

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

## Datei 10_linux 
## Variable CLASS
## at then 
## 
CLASS="--class gnu-linux ..... --unrestricted" 

update-grub 

```
  
## Documentation 

  * http://schulung.t3isp.de/documents/linux-security.pdf
  * Wrong concerning nmap in document
    * : -T5 = insane (quickest option, less accuracy, o.k ?)
    * should be -T5 = insane (most dangerous option, because it can kill running processes on target machine) 
