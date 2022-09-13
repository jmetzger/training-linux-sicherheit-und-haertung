# Besondere Fileattribute 

## Datei immutable machen 

  * Kann nicht gelöscht oder verändert 
  * geht auch für Verzeichnisse

```
cd /root
touch meindatei 
chattr +i meindatei
# Diese Datei kann jetzt nicht gelöscht oder verändert
# auch nicht unbenannt 
lsattr meindatei

# Heilen mit 
# D.h. root kann das auch wieder rausnehme
# Schutz vor mir selbst ;o) 
chattr -i meindatei
```

```
# Verzeichnisse
cd /root
mkdir meinverzeichnis
chattr +i meinverzeichnis
cd meinverzeichnis
# wichtig Option -d nehmen 
lsattr -d . 
# Jetzt können keine neuen Dateien angelegt werden
# oder gelöscht werden
# aber bestehende Dateien können inhaltlich geändert werden
```
