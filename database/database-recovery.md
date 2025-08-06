# Disaster Recovery

## RTO & RPO
**Recovery Time Objective** - max time to bring resources online
**Recovery Point Objective** - max amout of data loss
if 15mins RTO, its ok to restore current outage from backup 15mins ago
business decides. define at:
- component level and overall architecture level 
- different for HA and DR 

**High Availability events** - localised, easier to recover from
**Disaster Recovery event** - regional, take hours or longer

PAAS - HADR options built in

## Cluster Mechanism
built on
- Windows Server Failover Cluster (WSFC)
- Pacemaker (Linux)

**Failover Cluster Instances** configured on installation. Can't convert.