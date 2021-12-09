# Hardening apache (Centos 8) 

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

## Disabled directory listing (Version 1: Best solution) 

  * Please use this !!!, if you do not need diretory listing at all on server 

```
# Testing from other machine 
# you should not see a directory listing 
curl http://192.168.33.10/icons/ 

## Step 1 ## 
# in /etc/httpd/conf.modules.d/00-base.conf 
# find line 
LoadModule autoindex_module modules/mod_autoindex.so

# and comment it
#LoadModule autoindex_module modules/mod_autoindex.so

## Step 2 ## 
# overwrite autoindex.conf in /etc/httpd/conf.d 
# Why ? to be sure, that update process, does not create 
echo " " > /etc/httpd/conf.d/autoindex.conf 

## Step 3 ## 
# restart 
systemctl restart httpd 

## Step 4 ## 
# finally test from other server
curl http://192.168.33.10/icons/ 

```

## Disable directory listing on Directory - Level (Version 1: Best solution) 


```
# This is needed, because Directory Indexing is activated
# for icons folder within /etc/httpd/conf.d/autoindex.conf

# /etc/httpd/conf.d/z_security.conf 
Options -Indexes

<Directory "/usr/share/httpd/icons">
    Options -Indexes
</Directory>

systemctl reload httpd 

# verify with browser 
curl http://192.168.33.10 

```

## Harden error-pages 

```
ErrorDocument 404 " "
ErrorDocument 401 " "
ErrorDocument 403 " "
ErrorDocument 500 " "
```

## Disable modules not used 

```
# Examples 
/etc/conf.modules.d
00-dav.conf
00-lua.conf

# disable by overwriting file 
# Test it before that by disabling 
cd /etc/conf.modules.d/
echo " " > 00-dav.conf 
echo " " > 00-lua.conf 

systemctl restart httpd 
```

## If .htaccess is not needed, disable it altogether

```
1. Improves security (user cannot break system) 
2. Better for performance 
```

```
# 1. How to test 
echo "test" > /var/www/html/test.html 
echo "really-unknown-config" >> /var/www/html/.htaccess

curl -I http://192.168.33.10/test.html 
# if it is working (should not), you will get a 500 Status Code 
# --> Then you have to disable it 
 curl -I http://192.168.33.10/test.html
HTTP/1.1 500 Internal Server Error                                      Date: Thu, 09 Dec 2021 14:43:16 GMT                                     Server: Apache
Connection: close
Content-Type: text/html; charset=iso-8859-1

# In this case -> disable it 
# /etc/httpd/conf.d/z_security.conf 
<Directory /var/www/html/>
AllowOverride None   # .htaccess is simply ignored 
</Directory>

```

## Reference 

  * https://httpd.apache.org/docs/2.4/de/mod/core.html#serversignature
