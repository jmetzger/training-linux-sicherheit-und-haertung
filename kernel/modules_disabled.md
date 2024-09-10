# Disable kernel modules loading 

## When ? 

  * Can be set after all modules are loaded
  * e.g. embedded systems

## Walkthrough 

```
sudo su -
modprobe i2c_dev
# entladen 
modprobe -vr i2c_dev
sysctl kernel.modules_disabled=1
```

```
# now try to load module 
#not working 
modprobe i2c_dev
```

```
# change kernel modules_disabled
# does not work 
sysctl kernel.modules_disabled=1
```

```
# reboot, after that it works again
reboot 
```

```
sudo su -
modprobe -vr i2c_dev
lsmod | grep i2c
```
