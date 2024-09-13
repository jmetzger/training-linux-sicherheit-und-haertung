# iptables overview 

## Overview 

![image](https://github.com/user-attachments/assets/ea2fc2b0-8739-4b3d-a71e-b162f03a636b)

## Default Chains 

  * iptables offers the following builtin chains

```
INPUT
OUTPUT
FORWARD
PREROUTING (Inspect packets as soon as they come in (table → nat = -t nat))
```

## Side-Note

```
PREROUTING: Triggered by the NF_IP_PRE_ROUTING hook.
INPUT: Triggered by the NF_IP_LOCAL_IN hook.
FORWARD: Triggered by the NF_IP_FORWARD hook.
OUTPUT: Triggered by the NF_IP_LOCAL_OUT hook.
POSTROUTING: Triggered by the NF_IP_POST_ROUTING hook.
```

## Tables 

  * Within the Chains (like triggers in the kernel), we have tables
  * They have a specific job
  * Not all tables are in all chains

### What Tables do we have ?

  * The 3 most important are

```
mangle
nat
filter 
```

## See all rules 

```
## -L : List rules.
## -v : Display detailed information. This option makes the list command show the interface name, the rule options, and the TOS masks. The packet and byte counters are also listed, with the suffix ‘K’, ‘M’ or ‘G’ for 1000, 1,000,000 and 1,000,000,000 multipliers respectively.
## -n : Display IP address and port in numeric format. Do not use DNS to resolve names. This will speed up listing.

iptables -L -n -v

## with line-numbers
## Important when deleting 
iptables -L -n -v --line-numbers
```

## Adding / Deleting Lines 

```
# example for input
```


## Flush all rules 

```
iptables -F
```

## Set rules persistent 

```
# not present anymore 
apt search iptables-save

# use netscript-ipfilter
apt install -y netscript-ipfilter
``` 

  * https://ncomputers.org/netscript

## Show / Set Default policy for Input 

```
# Set default policy of input to drop 
iptables -P INPUT DROP
# You will see this in the listing not
iptables -L
```

## Example 1: Activate Logging 


## Example 2: Redirect packets 


## Example 3: Filter ingoing traffic (allow only ssh + established) 


## Example 4: Do not allow traffic outgoing to 80/443 from machine 

