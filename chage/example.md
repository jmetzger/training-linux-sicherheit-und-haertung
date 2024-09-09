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

