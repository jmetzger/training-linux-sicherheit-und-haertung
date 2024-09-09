# Passwortänderung durchsetzen

## Example 

```
-d -> letzten Passwortänderung setzen
-E -> Account läuft nicht ab
-m -> minimale Änderung zwischen Passwortänderungen
-M -> Änderung nach maximal 2 Tagen
-W -> Warnung Tage vor nötiger Passwortänderung
```

```
chage -m 1 -M 2 -W 2 -d 2024-09-08 -E -1 training2
```

```
root@kurs-VirtualBox:/etc/security# chage -l  training2
Letzte Passwortänderung                                 : Sep 08, 2024
Passwort läuft ab                                       : Sep 10, 2024
Passwort inaktiv                                        : nie
Benutzerzugang läuft ab                                 : nie
Minimale Anzahl der Tage zwischen Passwortänderungen    : 1
Maximale Anzahl der Tage zwischen Passwortänderungen    : 2
Anzahl Tage, an denen vor Passwortablauf gewarnt wird   : 2
```

