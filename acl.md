# ACL's 

## Installation of tools 

```
apt install acl 
```

## Walkthrough 


```
1. Gemeinsamer Ordner heroes
````

```
groupadd -r heroes
mkdir -p /shared/mutants
chgrp heroes /shared/mutants
```

2. 3 Benutzer erstelle (sue gehört nicht der Gruppe an)
```
useradd sylar
useradd cheerleader
useradd sue
usermod -aG heroes sylar
usermod -aG heroes cheerleader
```

3. SGID - Bit setzen 
```
chmod g+ws,o=- /shared/mutants
```

4. Wechsel in sylar und cheerleader
```
su - sylar
echo "Sylar was here" >> /shared/mutants/victims
exit
```

``` 
su - cheerleader
echo "\nNix gut cheerleader war hier." >> /shared/mutants/victims
exit
```

5. Hat Sue Zugriff ? Verify that user sue has no access to the directory /shared/mutants and its files.
```
su - sue
cat /shared/mutants/victims
exit
```

6. Zugriff für Sue (files erstellen, lesen und modifizieren in /shared/mutants .
2 acls: 1x für default (neue files), 1x für zugriff 

```
setfacl -m d:u:sue:rwx /shared/mutants
setfacl -m u:sue:rwx /shared/mutants
setfacl -m u:sue:rw /shared/mutants/victims
getfacl /shared/mutants 
getfacl /shared/mutants/victims
```

```
# nun mit sue testen
su - sue
echo "kann ich jetzt ?" >> /shared/mutants/victims 
touch sue-gruppe
mkdir /shared/mutants/sue-gruppe-ver
exit 
```

7. Privates file von cheerleader /shared/mutants/private
   Zugriff von sylar verhindern

```
su - cheerleader

echo "privat" >> /shared/mutants/private
setfacl -m u:sylar:- /shared/mutants/private
getfacl /shared/mutants/private
exit

su - sylar

cat /shared/mutants/private
# cat: /shared/mutants/private: Permission denied
exit
```
