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

## Private IP Classes 
Private IP classes are designated ranges of private IP addresses, reserved for internal use within local networks and not routable on the public internet.  
The three private IP classes are: 
- Class A (10.0.0.0 to 10.255.255.255) for large orgnaisations  
- Class B (172.16.0.0 to 172.31.255.255) for medium sized  
- Class C (192.168.0.0 to 192.168.255.255) for home  