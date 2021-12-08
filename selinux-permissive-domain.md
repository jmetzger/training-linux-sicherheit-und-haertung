# Set single domains/types to permissive 

```
semanage permissive -a httpd_t
semodule -l | grep permissive
permissive_httpd_t 1.0 
permissivedomains 1.0.0
semanage permissive -d httpd_t
```
