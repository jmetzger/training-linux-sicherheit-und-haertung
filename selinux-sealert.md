# sealert 

## Prerequisites 

```
# Works on centos/redhat 
dnf whatprovides sealert 
dnf install -y setroubleshoot-server 
```

## Variant 1: Search audit.log altogether 

```
# When a problem occurs go for 
sealert -a /var/log/audit/audit.log > report.txt 
# After that look into report for solutions 
```

## Variant 2: Use only a subset of the audit log 

```
# filter with ausearch, e.g. 
ausearch -c httpd --raw > audata.log 
sealert -a audata.log > report2.txt 
```
