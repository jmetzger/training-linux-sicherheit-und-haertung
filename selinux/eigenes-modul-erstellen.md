# Eigenes Modul erstellen 

## Achtung: 

  * Dies funktioniert nur mit RHEL 9 und nicht mit Rocky 9
  * Rocky 9 produziert Fehler beim laden von rpm-Paketen aus dem Repo beim Ausführen der sepolicy - Befehlen

## Voraussetzung für die Übung 

```
dnf update
# dnf whatprovider sepolicy 


# Paket die im Test-Script verwendet werden 
dnf install -y curl nc 

```

## Testscript erstellen 

```
sudo su -
cd /usr/local/bin
vi runner<deinkuerzel>
```

```
#!/bin/bash

APP=runner<deinkuerzel>

if [ ! -d /var/log/$APP ]
then
  mkdir /var/log/$APP
fi

echo "my log" >> /var/log/$APP/logit

curl http://www.google.de > /dev/null

exec nc -l -p 8888
```
