# Set rules immutable 

```
# Während der Laufzeit auf immutable setzen
auditctl -e 2
```

```
# Now change it again
# normal mode 
# not working 
auditctl -e 1
# Operation not permitted 
```

```
# Try to set new rule
auditctl -a  always,exit -F dir=/home -F perm=war -k file_del
```

```
# The audit system is in immutable mode, no rule changes allowed
```
