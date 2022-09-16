# Lynis Security Scanner 

## Walkthrough 

```
apt update 
apt install -y lynis 
lynis audit system 

# After that you analyse the report.
# View or compile the results like so:

# Scanning process wil also be documented on /var/log/lynis.log 
grep -E "^warning|^suggestion" /var/log/lynis-report.dat

```

