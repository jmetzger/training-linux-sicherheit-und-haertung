# Installation mit SecureBoot (tpm) 

## Einschränkung

  * Verschlüsselung mit tpm wird beim Installer noch nicht unterstützt

## Vorgehen 

  * Im BIOS: SecureBoot aktivieren
  * TPM2 aktivieren

## Bei der Installation 

  * Partition verschlüsseln (Verschlüsselung von LVM)
  * Passwort muss angegeben werden

## Was wird verwendet ?

  * Unter der Haube wird luks verwenden
  * In /etc/crypttab ist die entschlüsselung der Systempartition hinterlegt

## Manuell Anbindung an tpm 

```
# Ist secure boot 
mokutil --sb-state 

# clevis
apt install -y clevis-systemd clevis-luks clevis-tpm2 clevis-initramfs cryptsetup-bin mokutil
systemd-cryptenroll /dev/sda3
```

```
tpm2_pcrread
tpm2_getcap properties-fixed
tpm2_getcap properties-variable
tpm2_pcrread sha256
tpm2_pcrread sha256:7
```

```
ls -la /dev/tp*
crw-rw---- 1 tss root  10,   224 Sep 13 08:33 /dev/tpm0
crw-rw---- 1 tss tss  253, 65536 Sep 13 08:33 /dev/tpmrm0
```

```
# Device ausfinding machen, das verschlüsselt und lvm im Bauch hat
lsblk 

clevis luks bind -d /dev/sda3 tpm2 '{ "pcr_bank":"sha256", "pcr_ids":"7"}'

# falls nicht eingehängt, kann man das testen
# Bei uns Fehler, weil / schon gemountet ist 
clevis luks unlock -d /dev/sda3
```

```
# Prüfung ob askpass aktiviert ist
systemctl status clevis-luks-askpass.path
```

```
# Folgender Eintrag muss in der Cryptsetup sein
cat /etc/crypttab
dm_crypt-0 UUID=14959c59-1db3-4a19-bfb0-e494edea07c2 none luks
```

```
# Informationen in die initramfs eintragen
update-initramfs -u -k all
```

```
# Have a look if new slot was used
systemd-cryptenroll /dev/sda3
```

```
#SLOT TYPE
#   0 password
#   1 password
#   2 other
```

```
# Reboot
```



