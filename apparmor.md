# Apparmor


## How does it work ?

``` In practice

o apparmor is registered in the kernel (lsm-module)
o the kernel queries AppArmor before each system call
 ->to know whether the process is authorized to do the given
operation.
```

## Install 

```
# tools installed
dpkg -l | grep apparmor-utils 

Set up utilities you need for management
sudo apt install apparmor-utils
```

## Systemd 

```
# apparmor rules loaded ? 

# Loads rules into the kernel 
# from the profile 
systemctl start apparmor 

# Unloads the rules from the kernel 
systemctl stop apparmor 

```

## Profiles and Logging

```
# Profiles are in 
/etc/apparmor.d/

# Default logging will be to 
cat /etc/apparmor/logprof.conf  | grep logfiles
```

## Status 

```
Show the current status of apparmor
sudo apparmor_status
# or
sudo aa_status
```

## Profiles and additional profiles 

```
Set up additional profiles

Within the core installation
there are only a minimal number of profiles

So:

apt install apparmor-profiles
# Achtung, diese sind teilweise experimentell 
apt install apparmor-profiles-extra 

```

## Enable/Disable a profile 

```
# Disable a profile altogether
sudo ln -s /etc/apparmor.d/<profile> /etc/apparmor/disable/

# rereads that single profile
sudo apparmor_parser -R /etc/apparmor.d/<profile>

# Re-Enable a disabled profile
sudo rm /etc/apparmor.de/disable/<profile>
cat /etc/apparmor.d/<profile> | sudo apparmor_parser -a
```

## Wichtige Befehle:

```
aa-enabled	simple Abfrage, ob AppArmor aktiviert ist
aa-status	Überblick über die geladenen AppArmor-Profile mit Angabe des Modus
aa-unconfined	Ausgabe der Prozesse mit Netzwerkzugriff ohne Profil
aa-audit	Profil in den Audit-Modus versetzen
aa-complain	Profil in den Complain-Modus versetzen
aa-enforce	Profil in den Enforce-Modus versetzen
aa-autodep	Erstellung eines Basis-Profils im Complain-Modus
aa-genprof	Erstellung eines Basis-Profils mit interaktiver Ergänzung von Regeln und abschließender Versetzung des Profils in den Enforce-Modus
aa-logprof	interaktive Ergänzung von Regeln anhand der Einträge in /var/log/syslog
aa-cleanprof	automatisches Aufräumen eines Profils
```


## Apparmor aktivieren (Kernel) - just in case (ältere Versionen) 

```
# Dies ist ab Debian 10 und Ubuntu x 
# bereits der Fall
Enable AppArmor
If you are using Debian 10 "Buster" or newer, AppArmor is enabled by default so you can skip this step.

The AppArmor Linux Security Modules (LSM) must be enabled from the linux kernel command line in the bootloader:


$ sudo mkdir -p /etc/default/grub.d
$ echo 'GRUB_CMDLINE_LINUX_DEFAULT="$GRUB_CMDLINE_LINUX_DEFAULT apparmor=1 security=apparmor"' \
  | sudo tee /etc/default/grub.d/apparmor.cfg
$ sudo update-grub
$ sudo reboot
```



## Reference 

  * https://wiki.debian.org/AppArmor/HowToUse
