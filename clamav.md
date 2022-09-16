# Virenscanner clamav (Ubuntu 22.04)

## Komponenten 

```
clamav - client 
clamav-daemon - daemon
clamav-fresclam - service -> Dienst der die Virensignaturen aktualisiert 
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

  * Virendatenbank wird in /var/lib/freshclam gespeichert. 
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
