# Virenscanner clamav (Ubuntu 22.04)

## Komponenten 

```
clamav - client 
clamav-daemon - daemon
clamav-freshclam - service -> Dienst der die Virensignaturen aktualisiert 
```

## Wichtige clamscan Kommandos 

```
clamscan - Optionen
Option	Beschreibung
-i oder --infected	Gibt nur infizierte Dateien aus (und nicht alle Dateien die gescannt werden).
--remove	Entfernt infizierte Dateien. Mit Vorsicht benutzen!
--move=VERZEICHNIS	Verschiebt alle infizierten Dateien in das Verzeichnis VERZEICHNIS.
-r oder --recursive	Scannt Unterverzeichnisse rekursiv.
--no-archive	Alle Archiv-Dateien werden nicht gescannt.
-h oder --help	Zeigt alle Optionen von clamscan an.
```

## Virendatenbank 

  * Virendatenbank wird in /var/lib/clamav gespeichert. 
  * Aktualisierung durch den clamav-freshclam - Dienst oder manuell: freshclam 

## Aktualisierung durch Dienst 

```
# Konfiguration unter des Dienstes (clamav-freshclam) unter:
/etc/clamav/freshclam.conf 

# Dies kann auch so erfolgen
dpkg-reconfigure clamav-freshclam

# Frequenz 
Festlegen wie oft runtergeladen wird -> voreingestellt ist 24 mal am Tag.
```

## Dienste enablen 

```
systemctl enable clamav-freshclam
```


## Virendatenbank manuell aktualisieren.

```
# Dienst darf dafür nicht laufen, weil er ein LOCK hält 
systemctl stop clamav-freshclam
freshclam
systemctl start clamav-freshclam 
```

## Installation / Walkthrough (clamav-daemon)

```
apt install -y clamav clamav-daemon
# Achtung: Der Daemon läuft erst wenn die Virensignatur 1x runtergeladen worden sind
ä daemon ist bereits enabled bei nach Installation 
systemctl status clamav-daemon
systemctl status clamav-freshclam

```

## Privaten Mirror einrichten 

```
# Auf dediziertem Server
#!/bin/bash 
apt update
apt install -y python3 pip apache2 
pip3 install cvdupdate 
cvd config set --dbdir=/var/www/html
# better set this up as cron 
cvd update 
```

```
# In freshclam verwenden 
# /etc/clamav/freshclam.conf 
PrivateMirror=http://46.101.158.176
systemctl restart clamav-freshclam 

# Oder dpkg-reconfigure clamav-freshclam 

```



## Testen 

```
wget -P /tmp https://secure.eicar.org/eicar_com.zip
# clamscan -ir /tmp
# better: so you can see what is going on:
clamscan --debug -vir /tmp

# cpu schonender - nice - nice 15 -> niedrigste Priorität  
# nice -n 15 clamscan && clamscan -ir /tmp
```

## clamscan return - codes 

```
0 : No virus found.
1 : Virus(es) found.
2 : Some error(s) occurred.
```

## Variante 1: on access scanning (clamonacc) 

  * https://gist.github.com/ChadDevOps/dc5428e8d816344f68b03c99359731f9

### Schritt 1: config ändern 

```
vi /etc/clamav/clamd.conf 
```

```
# Anhängen
BytecodeTimeout 60000
OnAccessMaxFileSize 5M
OnAccessMountPath /home
OnAccessIncludePath /home
OnAccessExcludeUname root
OnAccessPrevention true
OnAccessExtraScanning false
VirusEvent /etc/clamav/detected.sh
OnAccessExcludeRootUID yes
OnAccessRetryAttempts 3
```

## Schritt 2: Unit ändern 

```
systemctl edit --full clamav-clamonacc.service
```

```
# --fdpass einfügen
# >
# See: https://medium.com/@aaronbrighton/installation-configuration-of-clamav-a>

[Unit]
Description=ClamAV On-Access Scanner
Documentation=man:clamonacc(8) man:clamd.conf(5) https://docs.clamav.net/
Requires=clamav-daemon.service
After=clamav-daemon.service syslog.target network.target

[Service]
Type=simple
User=root
ExecStartPre=/bin/bash -c "while [ ! -S /run/clamav/clamd.ctl ]; do sleep 1; do>
ExecStart=/usr/sbin/clamonacc --fdpass -F --log=/var/log/clamav/clamonacc.log ->

[Install]
WantedBy=multi-user.target
```

```
systemctl restart clamav-clamonacc.service
```



## Variante 2:  on access scannning without changing service 

```
vi /etc/clamav/clamd.conf
```

```
BytecodeTimeout 60000
OnAccessMaxFileSize 5M
OnAccessMountPath /home
OnAccessIncludePath /home
OnAccessExcludeUname root
OnAccessPrevention true
OnAccessExtraScanning false
VirusEvent /etc/clamav/detected.sh
OnAccessExcludeRootUID yes
OnAccessRetryAttempts 3
OnAccessExcludeUID 0
```

```
systemctl restart clamav-clamonacc.service
```



