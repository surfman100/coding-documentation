# Azure Virtual Machines


## Availability 
Need a strategy for
- unplanned hardware maintenance: event created by Azure for expected failure 
- unexpected downtime  
- planned maintenance: periodic by MS  
Think about reprovisioning

## Availability Set
VMs in an availability set have same s/w, same function (ie seperate by Web, App, DB etc)  
on failure only some of these machines are affected  
Need to select this option on VM creation 
Add a Load balancer

**Update Domain** - grouping of VMs for a service upgrade. by default 5 of these, up to 20 
**Fault Domain** - physical units of failure, nodes on same rack. So Update domains span fault domains 

## Availability Zone
With availability zone, you create select the zone or let Azure do this 

## Virtual Machine Scale Set 
You can attach **identical** VMs to this 
Automatic scaling and performance optimisation , true autoscaling 
Spreading Algorithim
- max spreading -> as many fault domains as possible  
- fixed spreading -> 5 (if 5 available!)
- auto scale rules  
Scaling rules 
- manual
- autoscale (set min, max, initial)


## Scaling  
Vertical -> up the size of VM etc during week, down at weekend


## App Service Autoscale
Price plan affects
- Stageing slots: 0,5,20
- Auto Scale: manual, rules, rules/elastic
- scale instanaces: 3,10,30 

**Deployment Slots** have their own hostnames
Swapped settings vs slot specific settings  
Security: 
- use app or
- use app service. configure provider to be the app registration 
Backups worth implementing....easy restore
- partial available