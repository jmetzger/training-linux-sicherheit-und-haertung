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

## Walkthrough (Centos 8/Redhat 8)

```
# root do 
dnf install -y perl git 
cd /root  
git clone https://github.com/sullo/nikto
cd nikto/program 
```

