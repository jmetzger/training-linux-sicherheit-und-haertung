# Password Quality 

## Set in /etc/security/pwquality.conf 

   * module pwquality musst be used in pam

```
# Ubuntu
cat /etc/pam.d/common-password | grep "pwquality" 
```


```
# mindestens 10 Zeichen (+1 wenn mindestens ein credit gesetzt ist
minlen = 11
ucredit = -2
ocredit = -2
enforcing = 1
enforce_for_root
```
