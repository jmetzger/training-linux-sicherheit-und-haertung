# Hardening apache 

## Prerequisites 

```
# php should be installed - to see how to secure it
dnf install -y php 
echo "<?php phpinfo(); ?>" > /var/www/html/info.php 

# 
mkdir /var/www/html/daten 
touch /var/www/html/daten/datei1.html
touch /var/www/html/daten/datei2.html 

```

## Testing with curl 

```
curl -I http://192.168.33.10 

curl -I http://192.168.33.10/info.php 
```

## Be sure to restrict communication (headers) 

```
#vi /etc/httpd/conf.d/z_security.conf 
ServerTokens prod 

# also disable server signature,
# just to be sure, it will ap
# But this should already be the case by default 
ServerSignature off
```

## Restrict information from php (Centos 8 with php-fpm) 

```
grep -r php_expose /etc 
#vi /etc/php.ini
# find line with php_expose = On 
# replace by 
php_expose = off 

# to take effect reload php-fpm service 
systemctl list-units | grep php 
systemctl reload php-fpm # reload is sufficient 

# and finally check from other server 
curl -I http://192.168.33.10/info.php 
# no php-version sould be visible with X- header 
```

## 


## Reference 

  * https://httpd.apache.org/docs/2.4/de/mod/core.html#serversignature
