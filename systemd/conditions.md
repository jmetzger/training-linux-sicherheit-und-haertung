# Start obnly when condition is met 

```
# only start when selinux is present otherwice skipping
# Has to be in Unit Section
[Unit]
ConditionSecurity=selinux

```
