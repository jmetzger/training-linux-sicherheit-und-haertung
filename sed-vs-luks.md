# Self-Encrypted harddisk vs. LUKS 

## Advantages Self-Encrypted (Hard-Disk) 

  * Encryption/Decryption is quicker because done by disk itself by controller 
  * Transparent, once decrypted (can be used on any OS, because not OS specific)
  * Works directly with harddisk-passwd in BIOS
  * Can be integrated with TPM, but then with pre-boot (OS) - on Linux ?? 

## Disadvantages Self-Encrypted (Hard-Disk)

   * Only safe, after power off, till someone cann attack 
     * up to this, keys still are in Memory 
     * Attack szenarion (cold-boot)   

## Advantages LUKS 

   * Possible to not encrypt complete disk, but also files or partitions 
   * Can use TPM together with 
