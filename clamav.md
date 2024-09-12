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

## Virendatenbank manuell aktualisieren.

```
# Dienst darf dafür nicht laufen, weil er ein LOCK hält 
systemctl stop clamav-freshclam
freshclam
systemctl start clamav-freshclam 
```

## Installation / Walkthrough 

```
apt install -y clamav clamav-daemon
# Achtung: Der Daemon läuft erst wenn die Virensignatur 1x runtergeladen worden sind
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

## on access scanning (clamonacc) 

  * https://gist.github.com/ChadDevOps/dc5428e8d816344f68b03c99359731f9

```
# konfig in 
man clamd.conf 
vi /etc/clamav/clamd.conf 

# Wichtig: Service erstellen 
systemctl edit --full --force clamonacc.service
```
