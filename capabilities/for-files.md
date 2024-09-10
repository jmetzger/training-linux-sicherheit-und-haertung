# Capabilities for files 

## Which file capability do exist ?

  * Effective
  * Inheritable
  * Permitted

### Effective 

  * Das ist das was ein Process dann verwendet ab dem Start des Programms (files), z.B pin

```
get cap /bin/ping
# hier das e 
# /bin/ping cap_net_raw=ep


```

### Permitted 

  * Nicht standardmäßig beim Starten des Prozesses aktiviert
  * Der Prozess hat aber das Rechte dies Capability durch einen System-Call zu aktivieren (d.h. sinnvoll für Entwickler eines Programms)

### Inheritive 

  * Wird an die Kind - Prozesse, die geforkt vererbt.
