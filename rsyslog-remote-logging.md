# Rsyslog Remote logging / ssl 

## Works 

  * with rsyslog 6+ 
  * Tested with Debian 11 (bullseye) 

## Create certificates and put in both server and client 

```
# in /etc/pki/tls/certs/
# lab.crt, lab.key

## Main - Server - config 
```

## Configuration on Server 

```
apt install rsyslog-gnutls 

```

```
#/etc/rsyslog.d/main-tls.conf 
## Added for TLS support
# make gtls driver the default
# $DefaultNetstreamDriver gtls

# certificate files
$DefaultNetstreamDriverCAFile   /etc/pki/tls/certs/lab.crt
$DefaultNetstreamDriverCertFile /etc/pki/tls/certs/lab.crt
$DefaultNetstreamDriverKeyFile  /etc/pki/tls/certs/lab.key


# provides TCP syslog reception with encryption
module(load="imtcp" StreamDriver.Name="gtls" StreamDriver.Mode="1" StreamDriver.AuthMode="anon")
input(type="imtcp" port="6514" )
```

```
systemctl restart rsyslog 
```

## Configuration on Client 

```
apt install rsyslog-gnutls 

```

```
#/etc/rsyslog.d/secondary-tls.conf 
# This is the client side of the TLS encrypted rsyslog 

# certificate file, just the CA file for a client
$DefaultNetstreamDriverCAFile /etc/pki/tls/certs/lab.crt 

# set up action 
$DefaultNetstreamDriver gtls           #use the gnutls netstream driver 
$ActionSendStreamDriverMode 1          #require the use of tls
$ActionSendStreamDriverAuthMode anon   #the server is NOT authenticated
# send all messages 
*.* @@(o)main.example.com:6514  

```


```
systemctl restart rsyslog 
```

## Testing 

```
# on secondary
logger "Does this work" 

# check secondary 
/var/log/messages 

# check main 
/var/log/messages 

# <- should be in both log files 

