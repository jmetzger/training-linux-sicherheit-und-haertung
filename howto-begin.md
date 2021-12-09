# Howto begin (with a server) ? 

## Which services are running and are they needed ? 

```
lsof -i 
```

```
A. If not needed uninstall 

B. If needed, restrict 
o Do the need to listen to all interfaces ? (or restrict) 

```

## Protect single services

```
Strategy 1: Simple Start.

A. firewall (only specific in and outgoing traffic)

o Best: Ingress - Only incoming traffic from trusted sources 
o Egress: Only allow outgoing ports if needed (and only from needed sources (ip's)) 

B. What is this service allowed to on OS 

o SELinux -> are rules present // only specific files / only specific ports 

o Restrict configuration 
# Understand how each service can protected 
  o Who is allowed connect (restrict as much as possible) 
  o Encryption possible, which ciphers, which protocols (SSL, not SSLv2)
  o Only use modules, that are really necessary (disable everything) 
  o Acess to specific folders (apache) 
  o What does service propagate (Version-Nr, OS, Additional Data) -> Restrict 
  o Weak configuration settings (Protocol 1 - ssh)

C. harden OS 

D. Baselining (IDS) HIDS - Host Introduction 

E. Network Intrusion Detection 

Strategy 2: Use reports as a basis (OpenSCAP, OpenVAS, nikto, nmap) 


Strategy 3: per checklist (Telekom) 

```
