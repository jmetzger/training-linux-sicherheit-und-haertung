# Apache SSL with letsencrypt ssl 

## Step 1: setup virtual host 

```
# /etc/httpd/conf/httpd.conf 
IncludeOptional sites-enabled/*.conf

```


```
#  
#  dx.t3isp.de 
<VirtualHost *:80>
    ServerName www.example.com
    ServerAlias example.com
    DocumentRoot /var/www/example.com/html
    ErrorLog /var/www/example.com/log/error.log
    CustomLog /var/www/example.com/log/requests.log combined
</VirtualHost>
```

## Refs:

  * https://www.digitalocean.com/community/tutorials/how-to-secure-apache-with-let-s-encrypt-on-centos-8
