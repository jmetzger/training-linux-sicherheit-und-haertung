# Restricting syscall with docker with seccomp

## Walkthrough

```
# Step 1: Download default.json 
# From:
# 
cd /usr/src 
wget https://raw.githubusercontent.com/docker/labs/master/security/seccomp/seccomp-profiles/default.json

# Step 2: remove chmod from syscall in json + rename file to no-chmod.json 

# Step 3:
docker run --rm -it --security-opt seccomp=no-chmod.json alpine sh
/ # chmod 777 /etc/services
chmod: /etc/services: Operation not permitted
```

## References 

  * https://docs.docker.com/engine/security/seccomp/
  * https://martinheinz.dev/blog/41
