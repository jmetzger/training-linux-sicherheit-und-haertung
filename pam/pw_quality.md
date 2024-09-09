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
# mindestens 2 große Zeichen (upper)
ucredit = -2
# mindestens 2 Sonderzeichen 
ocredit = -2
# Default 
enforcing = 1
# führt es auch auch für normale Nutzern nicht durch, wenn Bedingungen nicht erfüllt sind 
enforce_for_root
```
