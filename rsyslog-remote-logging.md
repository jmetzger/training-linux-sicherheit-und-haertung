# Rsyslog Remote logging / ssl 

## Works 

  * with rsyslog 6+ 
  * Tested with Debian 11 (bullseye) 

## Main - Server - config 

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
