# Eigenes Modul erstellen 

## Achtung: 

  * Dies funktioniert nur mit RHEL 9 und nicht mit Rocky 9
  * Rocky 9 produziert Fehler beim laden von rpm-Paketen aus dem Repo beim Ausführen der sepolicy - Befehlen

## Voraussetzung für die Übung 

```
dnf update
# dnf whatprovider sepolicy 
dnf install -y policycoreutils-devel

# Paket die im Test-Script verwendet werden 
dnf install -y curl nc rpm-build 
```

## Testscript erstellen 

```
sudo su -
cd /usr/local/bin
vi runner<deinkuerzel>.sh
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

```
chmod u+x runner<deinkuerzel>.sh
```

## 2. Session 

```
# unconfined 
ps auxZ | grep nc
```

## Erstellung 

```
cd
mkdir project-runner<kuerzel>
cd project-runner<kuerzel>
sepolicy generate --name runnerjme --application /usr/local/bin/runner<kuerzel>.sh
# Alternative
sepolicy generate --init /usr/local/bin/runner-<kuerzel>.sh 

```

```
## Er erstellt die ganzen Files

/usr/local/bin/runnerjme.te # Type Enforcement file
/usr/local/bin/runnerjme.if # Interface file
/usr/local/bin/runnerjme.fc # File Contexts file
/usr/local/bin/runnerjme_selinux.spec # Spec file
/usr/local/bin/runnerjme.sh # Setup Script
```

```
# im Verzeichnis
./runnerjme.sh
# Erstellt: pp (fertiges policy file, src-rpm, noach/rpm)
# Erstellt manpage
# restorecon auf Basis der erstellten Context(i) 
```

## Documentation 
  
  * https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/9/html/using_selinux/writing-a-custom-selinux-policy_using-selinux
  * https://access.redhat.com/articles/6999267
  * man sepolicy
  * man sepolicy-generate

## Documentation (Droplet)

  * https://medium.com/@chatila/new-droplet-from-custom-image-red-hat-enterprise-linux-rhel-server-fe7b5dc12c8e
