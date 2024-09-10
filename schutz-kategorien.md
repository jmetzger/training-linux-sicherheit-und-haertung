# Schutzkategorien 

```
o Physischer Zugriff
o Logging 
o Auditing and Detection 

IDS-System 
o HIDS 
  AIDE, Tripwire, OSSEC 
o NIDS 
  Snort
  Suricata 

o Application Security 
  o Local Applications 
    - Patch/Update Often 
    - Subscribe to Errate (bug/patch notifications)
    - Automated Software/System Patching 

  o Resource Access Control 
    o Principle of least privilege 
      - sudo 
      - run0 
      Access Controls 
      - SSH Configuration 
      - ACL 

o Kernel Vulnerabilities 
   - Kernel and Userspace 

   .> Root Kits 
      Escalate privileges to root 
      Load Kernel modules to hide the rootkit 
      Remove all traces of the rootkit 

    Solution: Remove possibility to load modules 

    -> kernel.modules_disabled = 1 

    Can only be set to 0 


o Authentication 

o Local System Security

o Network Security 

o Network Services Security 

o Denial of Service 

o Remote Access 

  o SSH 

o Firewalling and Packet Filtering

```
