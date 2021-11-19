# Apparmor


## How it works ?

``` In practice
 -> the kernel queries AppArmor before each system call
 ->to know whether the process is authorized to do the given
operation.
Set up utilities you need for management
sudo apt-get install apparmor-utils
```

## Install 

```
Set up utilities you need for management
sudo apt-get install apparmor-utils
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

## Reference 

  * https://wiki.debian.org/AppArmor/HowToUse
