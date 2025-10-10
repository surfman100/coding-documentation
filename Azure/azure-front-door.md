# Azure Front Door 
Is a CDN, think Security & Delivery. 
- **Load Balancing**: traffic distributed evenly   
- **Content Delivery**: caches and distributing of conetent to reduce latency  

- 118 edge locations 
- certificate management 

## Terminology 
- **SSL Termination** offloads SSL descryption from backend servers  
- **WAF** protection against common web vulnerabilities (SQL injection, attacks) 

## Load balancing options
| Load Balancer | Globa/Regional | HTTP(S) | Good for | 
| --- | --- | --- | --- | 
| Front Door | G | HTTP(S) | CDN, Edge locations |
| API Management | R or G | HTTP(S) Apis | |
| Application Gateway | R | HTTP(S) | load balancing and web app firewall. Transistioning to public in a region. PAAS, IAAS, OnPrem | 
| Load Balancer | R or G | Non-HTTP(S) | inside vnet, high performance | 
| Traffic Manager | G | Non-HTTP(S) | 

**Layer 7** : https traffic, ssl offload, web application firewall, path based, session affinity   
**Layer 4** : TCP & UDP, DNS based services  

Azure Front Door terminates connections at points of presence (PoPs) near to the client and establishes separate long-lived connections to the origins  
Possible to put Azure Traffic in front to reroute traffic if Front door goes down 

![Load Balancing Decision Tree](/azure/load-balancing-decision-tree.png)

## Tier differences 
|  | Standard | Premium |
| --- | --- | --- |
| Bot protection | no | yes | 
| private link | no | yes | 
| m/s managed rule set | no | yes |
| WAF report | no | yes | 
