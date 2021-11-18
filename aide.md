# Aide (Debian/Ubuntu) 

## Install

```
apt install aide
# adjust config 
# /etc/aide.conf /etc/aide.conf.d <- rules 
aideinit 

# No necessary on Debian / Ubuntu 
# aideinit does this 
# mv /var/lib/aide/aide.db.new.gz /var/lib/aide/aide.db.gz
```

## Backup 

```
tar czvf initial-aide.tgz /etc/aide/aide.conf /usr/bin/aide /var/lib/aide/aide.db.new
```

## Simulate modification 

```
echo "11.11.11.11 bad.host.com bad" >> /etc/hosts
```

## Do the check 

```
# In Ubuntu like so 
aide.wrapper --check

# In Debian like so
aide --check --config=/etc/aide/aide.conf
```
## Check is done on a daily basis 

  * /etc/cron.daily/aide 
