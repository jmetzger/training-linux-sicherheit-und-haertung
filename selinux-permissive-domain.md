# Set single domains/types to permissive 

## Walkthrough 

### Identify domain/type in Rocky/RHEL 

```
dnf install httpd
systemctl start httpd
firewall-cmd --add-service=http
```

```
cd /var/www/html
echo "hallo welt" >> welt.html
chcon -t var_t welt.html 
```

```
Im Browser öffnen -> permission denied
```

```
ps auxZ | grep httpd 
```

```
semanage permissive -a httpd_t
```

```
Im browser testen -> geht jetzt 
```

```
semodule -l | grep permissive
```

```
permissive_httpd_t 1.0 
permissivedomains 1.0.0
```

```
# wieder scharf schalten 
semanage permissive -d httpd_t
```

## Reference 

  * https://selinuxproject.org/page/PermissiveDomainRecipe
