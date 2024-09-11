# Scan for rootkits with rkhunter 

## versioncheck and update definitions 

### Set rkhunter.conf accordingly 

```
/etc/rkhunter.conf
```

```
# Set like so to make updates possile 
UPDATE_MIRRORS=1
MIRRORS_MODE=0
WEB_CMD=""
```

## Versioncheck Software / Update definitions 

```
rkhunter --versioncheck
rkhunter --update
```

## Scan 

```
rkhunter -c
# Logs in
/var/log/rkhunter.log 
```
