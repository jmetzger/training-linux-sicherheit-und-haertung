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
<VirtualHost *:80>
    ServerName www.ap1.t3isp.de
    ServerAlias ap1.t3isp.de
    DocumentRoot /var/www/ap1.t3isp.de/html
    ErrorLog /var/log/httpd/ap1-t3isp-de-error.log
    CustomLog /var/log/httpd/ap1-t3isp-de-access.log combined
</VirtualHost>
```

## Refs:

  * https://www.digitalocean.com/community/tutorials/how-to-secure-apache-with-let-s-encrypt-on-centos-8
