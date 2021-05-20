# Hacking I (unprivileged permissions) 

## Prepare the target (metasploitable 2) 

```
# metasploitable 2 should be up and running 

# Step 1:

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





## Ref: (normal privileges)

  * https://null-byte.wonderhowto.com/how-to/exploit-shellshock-web-server-using-metasploit-0186084/

## Ref: (root privileges)

  * https://samsclass.info/124/proj14/p18xLPE.htm
  
