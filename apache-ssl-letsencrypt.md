# Apache SSL with letsencrypt ssl 

## Step 0:

```
dnf install -y httpd 
systemctl enable httpd
systemctl start httpd 
```

## Step 1: setup virtual host 

```
# /etc/httpd/conf/httpd.conf 
IncludeOptional sites-enabled/*.conf

```

```
#  x = 1 to 7
#  apx.t3isp.de 
#  mx.t3isp.de
# mkdir /etc/httpd/sites-enabled
# cd /etc/httpd/sites-enabled 
# vi ap1.t3isp.de.conf 
<VirtualHost *:80>
    ServerName www.ap1.t3isp.de
    ServerAlias ap1.t3isp.de
    DocumentRoot /var/www/ap1.t3isp.de/html
    ErrorLog /var/log/httpd/ap1-t3isp-de-error.log
    CustomLog /var/log/httpd/ap1-t3isp-de-access.log combined
</VirtualHost>
```

```
/var/www
mkdir -p ap1.t3isp.de/html
cd ap1.t3isp.de/html/
echo "ich bin ap1 von jochen" > index.html
```

## Install certbot (Centos 8) 

```
dnf install -y epel-release 
dnf install -y certbot python3-certbot-apache mod_ssl

```


## Refs:

  * https://www.digitalocean.com/community/tutorials/how-to-secure-apache-with-let-s-encrypt-on-centos-8
