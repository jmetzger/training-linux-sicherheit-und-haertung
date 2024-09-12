# Systemd Analyze Example 

## Kommandos 

```
# Score für alle Dienste anzeigen 
systemd-analyze security
# Show possible settings to adjust for service ssh 
systemd-analyze security ssh 
```

## Walkthrough (Ubuntu9 

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
```






## Reference 

   * https://www.linux-magazin.de/ausgaben/2021/11/systemd-analyze/
