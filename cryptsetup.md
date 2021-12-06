# Cryptsetup 

```
lsblk
parted /dev/sdb
partprobe /dev/sdb
dnf install -y cryptsetup
cryptsetup luksFormat /dev/sdb1
cryptsetup luksOpen /dev/sdb1 secret-disk
ls -la /dev/mapper/secret-disk
mkfs.ext4 /dev/mapper/secret-disk
mkdir /mnt/secret
mount /dev/mapper/secret-disk /mnt/secret
echo "/dev/mapper/secret-disk /mnt/secret    ext4   defaults    1 2" >> /etc/fstab
umount /mnt/secret/
mount -av
```
