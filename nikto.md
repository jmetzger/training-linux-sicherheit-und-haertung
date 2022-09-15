# Nikto vulnerability scanner 

## Walkthrough (Debian / Ubuntu)  

```
# Teststellung
# main: 
apt install -y apache2
apt install -y php 
# vi /var/www/html
echo "<?php phpinfo(); ?>" > /var/www/html/info.php 
```

```
# Debian 10/Ubuntu 2x.04  
# secondary:
apt install nikto 
nikto -h http://main
```

## Walkthrough II (Debian / Ubuntu) 

```
# We detected, that Apache shows Version and Ubuntu -> Apache/2.4.xx (Ubuntu) 
# that's not what we want - let us fix this:

# main - Create new file 
#vi /etc/apache2/conf-available/z-security.conf 
#ServerTokens Prod 
a2enconf z-security 
systemctl reload apache 

# secondary 
nikto -h http://main
# or simply do a curl to check the headers
curl -I main 
```



## Walkthrough (Centos 8/Redhat 8)

```
# root do 
dnf install -y perl git 
cd /root  
git clone https://github.com/sullo/nikto
cd nikto/program 
```

