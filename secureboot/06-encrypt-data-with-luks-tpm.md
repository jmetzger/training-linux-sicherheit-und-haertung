# Encrypt data with Luks and tpm 

cd /
dd bs=1M count=1024 if=/dev/zero of=test.img
cryptsetup luksFormat --type luks2 test.img
cryptsetup open test.img test
cryptsetup close test

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
