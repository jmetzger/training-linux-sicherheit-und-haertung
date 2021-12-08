# SELinux

## Change context and restore it 
```
# Requirements - selinux must be enabled
# and auditd must run 
# find out 
getenforce 
systemctl status auditd

cd /var/www/html
echo "hallo welt" > welt.html 
chcon -t var_t welt.html
# includes context from welt.html 
ls -laZ welt.html
# when enforcing fehler beim aufruf im Browser 

# You can find log entries like so
cat /var/log/audit/audit.log
# show all entries caused by executable httpd 
ausearch -c httpd 

# herstellen auf basis der policies 
restorecon -vr /var/www/html 
```

## Analyze 

```
# Under which type/domain does httpd run 
ps auxZ | grep httpd

# What is the context of the file 
ls -Z /var/www/html/welt.html 

# So is http_t - domain allowed to access ?
sesearch --allow --source httpd_t --target httpd_sys_content_t --class file
sesearch -A -s httpd_t -t httpd_sys_content_t -C file 
# Yes !
# output
allow httpd_t httpd_sys_content_t:file { lock ioctl read getattr open
};
allow httpd_t httpdcontent:file { create link open append rename write
ioctl lock getattr unlink setattr read }; [ ( httpd_builtin_scripting
&& httpd_unified && httpd_enable_cgi ) ]:True
...
# so let's check
echo "<html><body>hello</body></html>" > /var/www/html/index.html
chmod 775 /var/www/html/index.html
# open in browser:
# e.g.
# http://<yourip>
# you should get an output -> hello ;o)
# Now change the type of the file
# ONLY changes temporarily
# NEXT restorecon breaks it.

chcon --type var_t /var/www/html/index.html
ls -Z /var/www/html/index.html
# open in browser again
# http://<yourip>
# NOW -> you should have a permission denied
# Why ? -> var_t is not one of the context the webserver domain
(http_t) is not authorized to connect to
# Doublecheck
sesearch --allow --source httpd_t --target var_t --class file
# -> no output here -> no access
# Restore again
restorecon -v /var/www/html/index.html
# output
# Relabeled /var/www/html/index.html from
unconfined_u:object_r:var_t:s0 to
unconfined_u:object_r:httpd_sys_content_t:s0
ls -Z /var/www/html/index.html
# output
unconfined_u:object_r:httpd_sys_content_t:s0 /var/www/html/index.html
# open in browser again
# http://<yourip>
# Now testpage works again
```

## Set single domains/types to permissive 

```
semanage permissive -a httpd_t
semodule -l | grep permissive
permissive_httpd_t 1.0 
permissivedomains 1.0.0
semanage permissive -d httpd_t
```


## Docs 

  * http://schulung.t3isp.de/documents/linux-security.pdf
