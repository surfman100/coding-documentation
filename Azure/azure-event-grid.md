# Azure Event Grid

publishers -> sends events -> subscriber 
events conform to **CloudEvents 1.0** specificiation  
event source e.g. Azure Storage is event source for blob created events 

## Topics
- system: you don't see but can subscribe too. 
- custom: 
- partner: 

Create a **subscription** to subscribe to a topic. Set an expiration date. 

## Retry
Can set maximum number of attempts  
Tries, then try again 30s later, then 3mins later, 5mins from last -> dead letter    
Set a dead letter queue (storage account) or event will be deleted  
Batch messages for throughput gains 