## Linux Malware Detection (maldet/LMD)

```
cd /usr/src
wget https://www.rfxn.com/downloads/maldetect-current.tar.gz
mkdir maldetect 
mv maldetect-current.tar.gz maldetect 
cd maldetect 
tar xvf maldetect-current.tar.gz 

```

```
cd /usr/src/maldetect/maldetect-1.6.5
./install.sh 

# version anzeigen
maldet 
# update der Signaturen
maldet -u 
# Update der Software
maldet -d 

# Evtl config anpassen wenn gewünscht.
# Standardmäßig erfolgt 1x nächtlich ein Scan 
# /usr/local/maldetect/conf.maldet 

wget -P /tmp https://secure.eicar.org/eicar_com.zip 
cd /tmp
cp -a eicar* /home/kurs
chown kurs:kurs /home/kurs/eicar*

maldet -a /home/kurs
# reportliste 
maldet -e 
```

```
# Als Service betreiben 
# vi /usr/local/maldetect/monitor_paths
/etc
/home 

# /usr/local/maldetect/conf.maldet 
# default_monitor_mode auf /usr/local... setzen 
# default_monitor_mode="users"
default_monitor_mode="/usr/local/maldetect/monitor_paths"

# 
apt install inotify-tools 

systemctl start maldet 

# Logs anschauen ob monitoring auf Pfade erfolgt 

# 2. Session auf machen als user 'kurs'
# und datei downloaden. 
wget https://secure.eicar.org/eicar_com.zip 

# 1. Session als root. logs beobachten
/usr/local/maldetect/logs/event_log 



```

## Monitoring Log inotify 

```
inotify monitoring log: /usr/local/maldetect/logs/inotify_log
```

