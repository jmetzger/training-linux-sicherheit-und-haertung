# Kernel Hardening 

## Hardening params 

```
# avoid live patching of kernel 
kernel.kexec_load_disabled=1

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
