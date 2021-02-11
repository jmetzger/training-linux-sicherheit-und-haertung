# Install metasploitable 2

## Ref:

  * https://securingninja.com/how-to-install-metasploitable-in-virtualbox/
  
## Setup ;o) Hacking Target (192.168.56.110)

```
cd /usr/lib/cgi-bin
# sudo hello.sh
#!/bin/bash
echo "Content-type: text/html"
echo ""
echo "Hello world!"
```

```
# chmod u+x is not sufficient 
chmod 755 hello.sh
```

## Start attack from Kali (192.168.56.109) 

```
# per ssh 
msfconsole
search shellshock 
etc.
```
