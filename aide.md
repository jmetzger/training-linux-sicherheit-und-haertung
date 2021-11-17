# Aide (Debian/Ubuntu) 

## Install

```
apt install aide
# adjust config 
# /etc/aide.conf /etc/aide.conf.d <- rules 
aideinit 

# To use it, we have to move it 
# Right position in Debian ? 
mv /var/lib/aide/aide.db.new.gz /var/lib/aide/aide.db.gz
```

## Backup 

```
tar czvf initial-aide.tgz /etc/aide/aide.conf /usr/bin/aide /var/lib/aide/aide.db.new
```

## Do the check 

```
aide.wrapper --check 
```
## Check is done on a daily basis 

  * /etc/cron.daily/aide 
