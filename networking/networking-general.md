# Networking General

## IP at work
find out what it is using:
- [WhatIsMyAddress](https://whatismyipaddress.com)
- NsLookup tool. ```nslookup myip.opendns.com resolver1.opendns.com```
- Powershell. ```(Invoke-WebRequest -Uri "https://ifconfig.me/ip").Content```
- Curl. ```curl ifconfig.me``` 

The external IP address you see is usually your company’s firewall, VPN, or proxy public IP — not your laptop’s individual one.

## Network bandwidth testing
Another tool [NTTTCP](https://learn.microsoft.com/en-us/azure/virtual-network/virtual-network-bandwidth-testing?tabs=windows)  
Install and run in *receive* and *send* mode  

**tracepath** shows all the hops to reach a destination 
