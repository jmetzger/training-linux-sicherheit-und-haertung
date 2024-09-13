# MOK -> mokutil 

## MOK 

  * machine owner keys

## MOK and UEFI 

  * When installing a distribution such as Ubuntu with secure boot activated, the installer creates a MOK key in the NVRAM which can be seen with ‘mokutil -l ’.
  * You can see it with mokutil -l
  * Not part of core UEFI - Specificatin.

```
The concept of MOK is not officially part of Microsoft's Secure Boot. It's implemented by Shim, a special loader that actually overrides the firmware's Secure Boot handling – it has its own signature verification code that allows MOK-signed loaders to completely bypass the built-in SB verification.

Therefore the MOK database is stored as an ordinary EFI NVRAM variable named MokList
```

## mokutil

  * Tool, um die Machine Owner Keys zu manipulieren
  * Reference: https://manpages.ubuntu.com/manpages/bionic/man1/mokutil.1.html

## Herausfinden, ob secure boot aktiviert ist 

```
mokutil sb-state
```
