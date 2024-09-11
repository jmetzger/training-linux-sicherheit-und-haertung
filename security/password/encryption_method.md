# Passwort Encryption method 

## Identified in shadow - file 

```
# Example
$6$xb......
```

```
$6$ identifies encryption algorithm for password
```

## How to set it 

```
/etc/login.defs
ENCRYPT_METHOD SHA512
```

## Reference 

  * https://manpages.debian.org/unstable/libcrypt-dev/crypt.5.en.html
