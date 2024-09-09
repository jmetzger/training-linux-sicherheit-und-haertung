# User Sperren / entsperren 

  * Sperrt Benutzung von Passwort 

```
usermod -L training2 
# macht ein ! vor das Passwort in /etc/shadow 
```

```
usermod -U training2 
# entfernt ! 
```
