# Exercise sudo 

## Übung 1a:
    
```
Neuer Benutzer "training" erstellen und der weiteren Gruppe sudo zuordnen
Standard: Heimatverzeichnis training usw. 
Testen (entweder neu einloggen oder in terminal su - training 
sudo dann testen 

- adduser  (interaktiv) 
- useradd (lowlevel - Befehl) 
```

```
adduser training
# der weiteren Gruppoe hinzufügen
usermod -aG sudo training

# testen mit dem neuen Benutzer 
su - training
# sudo testen
sudo su -
# passwort eingeben
```

## Übung 1b:

```    
Einen neuen Benutzer erstellen training2, der
nur den ssh-daemon neu starten darf 
(nicht mehr)
```

````
# als root
adduser training2 
echo "training2 ALL=(ALL:ALL) /bin/systemctl restart ssh" > /etc/sudoers.d/training2
chmod 440 /etc/sudoers.d/training2
## testen
su - training2
## hier keine status ausgabe, weil keine Berechtigung 
sudo systemctl restart ssh
exit // Ausgabe
# als root, hat es geklappt
journalctl -eu ssh
```
 
