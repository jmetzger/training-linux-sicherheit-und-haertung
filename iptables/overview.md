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
iptables -L -n -v
```

## Flush all rules 

```
iptables -F
```


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

