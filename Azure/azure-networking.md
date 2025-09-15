# Azure Networking Concepts

![Networking](/Azure/networking.gif)

| Resources | Description |
| --- | --- |
| VNet | Your private network in Azure for VMs |
| Subnets | division of VNet IP address ranges into smaller manageble segments |
| Express Route | Connects your local network with VNet |
| VNet Paring | Connects two VNets | 
| Private Link | Connects resources to the VNET eg Storage |
| Network Security Groups | secure resources within subnets |



## VNET
Private network in Azure for VMs    
Can't change address space after creation.  
Public IP's are not associated with a VNet, more on the resource itself (eg VM)

## Public IPs
Static - removed when resource deleted  
Dynamic - assigned on resource startup, released on shutdown  
Assigned to the NIC, Load Balancer, VPN Gateways and Application Gateways   

| Address | Association | Dynamic | Static |
| --- | --- | --- | --- |
| VM | NIC | Yes | Yes | 
| Load Balancer | Front end config | Yes | Yes |
| VPN Gateway | Gateway IP config | Yes | Yes* |
| App Gateway | Front end config | Yes | Yes* |

*certain SKUs

Public IP SKU differences (basic is being retired)
| Feature | Basic SKU | Standard SKU |
| --- | --- | --- | --- |
| IP Assignment | ipv4: Static/Dynamic ipv6: Dynamic | Static |
| Security | Open by Default. NSG optional | Secure by default, closed to inbound traffic. NSG is required |
| Resources | NICs, VPN GW, App GW, public LB | NICS or public LB |
| Resources | not zone redundant | zone redundant by default |
| Routing Preference | allows granular control | not supported |
| Standard LB | ipv4/6 support | not supported |
| NAT GW | ipv4 supported | not supported |
| Azure Firewall | ipv4 supported | not supported |

## Private IPs
| Address | Association | Dynamic | Static |
| --- | --- | --- | --- |
| VM | NIC | Yes | Yes | 
| Internal Load Balancer | Front end config | Yes | Yes |
| App Gateway | Front end config | Yes | Yes |

## VNet pairing 
Just a setting under one of the VNets  


## Azure DNS


## Azure Private Link
VNet to azure PAAS resource. Removes need for public IP.  


## Networking Concepts
CIDR notation: split the IP into route prefixins / host addressing.  
Remember 2^8 = 256  
192.0.2.1/24 = 24 (8 + 8 + 8) significants bits are the prefix, remaining 8 = host addressing = 2 pow (32 - 24) = 2 pow (8) = 256. 

## Subnet
NICs live within a subnet   
Contain a pool of IP's that the NIC's can use (pull from)  
Use subnets to divide our VNet  
e.g. 
| Resource | ipv4 | range
| --- | --- | --- |
| VNet | 10.0.0.0/24 | 10.0.0.0 -> 10.0.0.127 | 
| Subnet1 | 10.0.0.0/26 | 10.0.0.128 -> 10.0.0.191 | 
| Subnet1 | 10.0.0.0/26 | 10.0.0.192 -> 10.0.0.255 | 

A service might require or create their own subnet. (e.g. dedicated subnet needed for VPN Gateway)