# Encrypt data with Luks and tpm 

## Walkthrough 

```
1. Platte in virtualbox erstellen
2. hochfahren
```

```
# Device identifizieren
lsblk
# Platte formatieren mit parted z.B. 

# Verschlüsseln der Partition
cryptsetup luksFormat --type luks2 /dev/sdb1
cryptsetup open /dev/sdb1 test
# now available und /dev/mapper/test
mkfs.ext4 /dev/mapper/test
# testweise einhängen
mkdir /mnt/test
mount /dev/mapper/test /mnt/test 
umount /mnt/test



```

```
# Set in /etc/crypttab
echo "test /dev/sdb1 none" >> /etc/crypttab"
# find out uuid
lsblk -o name,uuid
# Get uuid of /dev/mapper/test
echo "UUID=f521fd74-e82a-41f9-9b95-4dc417d7f50b /mnt/test ext4 defaults 0 0" >> /etc/fstab
```

```
# Try to reboot, you need to enter password

```

```
# Now set tpm with systemd-cryptenroll
systemd-cryptenroll --tmp2-device /dev/tpmrm0 --tpm2-pcrs 7 /dev/sdb1
```

```
# Try to reboot, now you do not need to enter password
```




```
tpm2_getcap pcrs
tpm2_pcrread sha256
tpm2_pcrread sha256:7

systemd-cryptenroll /test.img
systemd-cryptenroll --tpm2-device /dev/tpmrm0 --tpm2-pcrs 7 /test.img
echo "test /test.img none" >> /etc/crypttab

cryptsetup open test.img test

# Does not work 
uuid=$(lsblk -o UUID /dev/mapper/test -n)
# figure it out manually 
echo $uuid

mkdir /mnt/test
mkfs.ext4 /dev/mapper/test
cd /mnt 
mount /dev/mapper/test test
cd test
ls -la
touch helloyou
reboot
```

```
# After reboot 
cd /mnt/test
ls -la
```
