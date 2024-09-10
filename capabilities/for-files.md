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

## Example ping 

```
# as unprivileged user
cd /usr/bin
sudo cp ping meinping
meinping www.google.de
```

```
meinping www.google.de
meinping: socktype: SOCK_RAW
meinping: socket: Vorgang nicht zulässig
meinping: => missing cap_net_raw+p capability or setuid?
```

```
sudo setcap CAP_NET_RAW=ep /usr/bin/meinping
meinping www.google.de
```

## man capabilities 
