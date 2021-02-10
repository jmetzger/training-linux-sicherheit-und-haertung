# SELinux

## Walkthrough 

```
# be sure selinux is activated
setenforce 1
ps -efZ | grep apache2
system_u:system_r:httpd_t:s0 root 9967 1 0 04:18 ?
00:00:00 /usr/sbin/apache2 -k start
touch /var/www/html/index.html
ls -Z /var/www/html/*
# output
unconfined_u:object_r:httpd_sys_content_t:s0 /var/www/html/index.html
# So is http_t - domain allowed to access ?
sesearch --allow --source httpd_t --target httpd_sys_content_t --class
file
# Yes !
2019/07/31 08:25 47/56
Training materials / Schulungsunterlagen - http://localhost/dokuwiki/
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

## setroubleshoot to find problems 

```
yum install setroubleshoot 
sealert -a /var/log/audit/audit.log 
# see how to fix 
```

## Create module 
```
setenforce 0
# replay situation, like opening page in webbrowser -> httpd 
# analyse logs 
ausearch -c 'httpd' --raw | audit2allow -M my-httpd
semodule -i my-httpd.pp
setenforce 1
# retest- should work now 
```

## Docs 

  * http://schulung.t3isp.de/documents/linux-security.pdf
