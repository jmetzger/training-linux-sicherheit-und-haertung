# MOK -> mokutil 

## MOK 

  * machine owner keys

## MOK and UEFI 

  * When installing a distribution such as Ubuntu with secure boot activated, the installer creates a MOK key in the NVRAM which can be seen with ‘mokutil -l ’.
  * You can see it with mokutil -l

## mokutil

  * Tool, um die Machine Owner Keys zu manipulieren
  * Reference: https://manpages.ubuntu.com/manpages/bionic/man1/mokutil.1.html

## Herausfinden, ob secure boot aktiviert ist 

```
mokutil sb-state
```
