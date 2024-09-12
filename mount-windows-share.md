# Mount Windows Share 

## Unencrypted 

### On Windows create share in C:\test 

```
# Allow for User ITS-Admin
# Pass: my@ver0secretpass 

```

```
# get primary network interface
# not the host only one 
ipconfig /all
```



### Setup Share 

```
sudo su -
mkdir /mnt/test
cd /mnt
mount -o username=ITS-Admin,password='my@ver0secretpass'  -t cifs //10.10.22.143/test test
```
