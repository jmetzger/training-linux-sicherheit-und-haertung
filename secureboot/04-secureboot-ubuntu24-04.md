# Installation mit SecureBoot (tpm) 

## Einschränkung

  * Verschlüsselung mit tpm wird beim Installer noch nicht unterstützt

## Vorgehen 

  * Im BIOS: SecureBoot aktivieren
  * TPM2 aktivieren

## Bei der Installation 

  * Partitiin verschlüsseln (Verschlüsselung von LVM)
  * Passwort muss angegeben werden

## Was wird verwendet ?

  * Unter der Haube wird luks verwenden
  * In /etc/crypttab ist die entschlüsselung der Systempartition hinterlegt 
