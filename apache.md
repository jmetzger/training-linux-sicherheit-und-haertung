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

## Reference 

  * 
