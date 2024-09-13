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


### Analyse:

  * Achtung: powershell - Befehle müssen als Administrator ausgeführt werden 

```
# In Linux sehen wir die Protokoll-Version
cat /proc/mounts | grep cifs
//10.10.22.143/test /mnt/test cifs rw,relatime,vers=3.1.1,cache=strict,username=ITS-Admin,uid=0,noforceuid,gid=0,noforcegid,addr=10.10.22.143,file_mode=0755,dir_mode=0755,seal,soft,nounix,serverino,mapposix,rsize=4194304,wsize=4194304,bsize=1048576,retrans=1,echo_interval=60,actimeo=1,closetimeo=1 0 0
```

```
# powershell ausführen als Administrator auf Windows 

# Auf Windows - Seite können wir die Verbindungen so einstellen, dass immer verschlüsselt wird (für den gesamten Server)
Set-SmbServerConfiguration –EncryptData $true
Get-SmbServerConfiguration 
### wichtig die Zeile
Get-SmbServerConfiguration
---> RejectUnencryptedAccess         : True
```


## Encrypted 

![image](https://github.com/user-attachments/assets/f9d4b9d4-d9f0-435d-b988-ce711e4914ac)

```
# Ein Share kann explzit so eingestellt werden, dass er encrypted ist bei der Übertragung
Set-SmbShare -Name test2 -EncryptData $true
```


```
# man sieht das dann auch in der config
Get-SmbShare -Name test2 
Get-SmbShare -Name test2 | Format-List -Property *

EncryptData           : True
```

```
# Auf Linux 
mount --verbose -o seal,username=ITS-Admin,password='P@ssw0rd'  -t cifs //10.10.22.143/test2 test
mount.cifs kernel mount options: ip=10.10.22.143,unc=\\10.10.22.143\test2,seal,user=ITS-Admin,pass=********
root@kurs-VirtualBox:/mnt# cat /proc/mounts | grep cifs
//10.10.22.143/test2 /mnt/test cifs rw,relatime,vers=3.1.1,cache=strict,username=ITS-Admin,uid=0,noforceuid,gid=0,noforcegid,addr=10.10.22.143,file_mode=0755,dir_mode=0755,seal,soft,nounix,serverino,mapposix,rsize=4194304,wsize=4194304,bsize=1048576,retrans=1,echo_interval=60,actimeo=1,closetimeo=1 0 0
```

```
Share mit Verschlüsselung erstellen
New-SmbShare –Name test5 -Path C:\test5 –EncryptData $true
```

```
# Linux
mount --verbose -o seal,username=ITS-Admin,password='P@ssw0rd'  -t cifs //10.10.22.143/test3 test
```

## Reference 

  * https://learn.microsoft.com/de-de/windows-server/storage/file-server/smb-security
