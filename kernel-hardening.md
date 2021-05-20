# Kernel Hardening 

## Hardening params 

```
# Prevent loading of modules after a specific timeframe after boot
kernel.modules_disabled=1

# Disable live patching 
kernel.kexec_load_disabled=1

# You are not using berkeley package filter
# disable loading of modules 
kernel.unprivileged_bpf_disabled=1
```

## Tools 

### Lockdown 

```
Interesting script to do some restrictions 

https://gitlab.com/taggart/lockdown
```
