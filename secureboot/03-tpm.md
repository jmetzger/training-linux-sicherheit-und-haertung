# tpm 2.0 

## Overview (Hierarchie)

### Endorsement Key (EK)

  * Eingebrannt, nicht lesbar, nicht veränderbar
  * Eindeutig pro TPM (2048bit Schlüssellänge)
  * Private and Public Part (Private Part will never leave the system)

### Storage Root Key (SRK)

  * Wurzel des TPM-Schlüsselbaumes
  * Lediglich zur Verschlüsselung weiterer Benutzer Schlüssel

### Attestation Identity Keys (AIK)

  * Dienen zum signieren von PCR werten (Flüchtiger Speicher)

## Sicherheitsfunktionen des TPM 

### Versiegelung (sealing)

```
Durch Bilden eines Hash-Wertes aus der System-Konfiguration (Hard- und Software)
können Daten an ein einziges TPM gebunden werden.

Hierbei werden die Daten mit diesem Hash-Wert verschlüsselt.
Eine Entschlüsselung gelingt nur, wenn der gleiche Hash-Wert wieder ermittelt wird 
```

  * Wichtig: Ein TPM kann mithilfe von PCR-Messungen (Platform Configuration Register) Richtlinien implementieren, die den nicht autorisierten Zugriff auf vertrauliche Daten beschränken. 

### Eigener Zufallsgenerator 

## PCR's (Platform C. Registers)

  * PCR sind register, die während der Laufzeit befüllt werden
  * Werden während der Laufzeit anhand von Messungen befehlt, die verschiedenen Register
  * 24 Register (jedes kann noch verschiedene Algorithm anbiet
  * Daten werden nur rausgegeben (Es können keys w

```
tpm2_pcrread 
```




## Commands 

### Show the tpm-devices 

```
ls -la /dev/tp* 
```


### tpm2-commands 

```
apt install -y tpm2-tools
```

```
# List all pcr's
tpm2-pcrread 
```
```
