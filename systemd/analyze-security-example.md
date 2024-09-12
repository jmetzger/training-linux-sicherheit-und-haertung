# Systemd Analyze Example 

## Kommandos 

```
# Score für alle Dienste anzeigen 
systemd-analyze security
# Show possible settings to adjust for service ssh 
systemd-analyze security ssh 
```

## Walkthrough (Ubuntu)

### Prerequisites 

```
apt install python3
```

### Step 1: Create HTML Page / Service 

```
sudo su -
mkdir /home/kurs/public
cd /home/kurs/public
vi index.html 
```

```
<!doctype html>
<html lang=en>
  <head>
    <meta charset=utf-8>
    <title>Welcome guys ! </title>
  </head>
  <body>
    <p><h1>What's up </h1></p>
  </body>
</html>
```

```
systemctl edit --full --force helloworld.service 
```

```
[Unit]
Description=Simple Http Server
Documentation=https://docs.python.org/3/library/http.server.html
[Service]
Type=simple
WorkingDirectory=/home/kurs/public
ExecStart=/usr/bin/python3 -m http.server 8080
ExecStop=/bin/kill -9 $MAINPID
[Install]
WantedBy=multi-user.target
```

```
systemctl start helloworld
systemd-analyze security helloworld
# -> 9.6. 
```

## Step 2: NoNewPrivileges 

```
systemctl edit --full helloworld
```

```
# add: Privilegien können nicht erhöht werden 
NoNewPrivileges=true
```

```
systemctl restart helloworld
systemd-analyze security helloworld 
```

## Step 3: PrivateTmp=yes && 



## Step 4: RestrictNamespaces=uts ipc pid user cgroup  

  * Prozess darf nicht auf dieses Namespaces zugreifen
  * net braucht er wg. 8080 - Binding 

```
--> 8.8.
Sinkt von UNSAFE auf EXPOSED
```

## Step 5: ProtectKernelTunables=yes && ProtectKernelModules=yes && ProtectControlGroups=yes

  * ProtectKernelTunables

```
> READONLY -> /proc/sys/«, »/sys«, »/proc/sysrq-trigger/«, »/proc/latency_stats/«, »/proc/acpi/«, »/proc/timer_stats/«, »/proc/fs/« »/proc/irq/« zugreifen kann, für den Prozess read-only 
```

  * ProtectKernelModules = yes

```
# Laden und Entladen verboten
```

  * ProtectControlGroups = yes

```
Zugriff auf die ControlGroups verboten
-> sowas braucht nur ContainerVerwaltungssoftware 
```

```
# Ergebnis: 8.1.
```

## Step 6: Capabilities 

```
CapabilityBoundingSet=CAP_NET_BIND_SERVICE CAP_DAC_READ_SEARCH 
# Ausgeschlossen wird dadurch »CAP_SYS_ADMIN«, »CAP_DAC_OVERRIDE« »CAP_SYS_PTRACE«
# Bringt viele Punkte
```

```
# Ergebnis: 6.1 -> MEDIUM 
```

## Sehr schöne Liste an Möglichkeiten 

   * https://gist.github.com/ageis/f5595e59b1cddb1513d1b425a323db04

## Reference 

   * https://www.linux-magazin.de/ausgaben/2021/11/systemd-analyze/
  
