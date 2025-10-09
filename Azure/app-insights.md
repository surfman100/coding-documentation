# Application Insights 

| Feature | Description |
| --- | --- |
| Live Metrics | Observer real time activity | 
| Availability | Test your application end points to test availability | 
| Usage | understand how users interact with application | 
| Smart Detection | Automatic failure and anomaly detection |
| Application Map | Visual health and view | 
| Distributed Tracing | Search and visualize end-to-end | 

## Availablity Testing  
create up to 100 
**Standard Test**: sends single request. includes SSL validity etc 
**Classic Test**: URL Ping or Multi Step test   
**Custom**: Create a custom application 

## Application Map 
Understand and do deep dive 

## Instrumenting application

| When / Where | Description | 
| --- | --- |
| Run Time | no update to code needed, app already deployed | 
| Dev Time | add App Insights to code. Customise and send more telemetry | 
| Web pages | for page view, ajax and other telemetry | 
| Mobile App | integrate with VS App Center | 
| Availability Tests | ping www regularly from our servers | 

code against **Application Insights** or **OpenTelemetry** API.  


## Metrics 
two kinds:

**Log based metrics**
translated into kusto queries from **stored events**
more dimensions, suitable for data analysis and ad-hoc diagnostics 
Use:
- automatically collected events 
- SDK to send events manually 
use sampling and filtering for high volume 

**Standard/Platform metrics**  
preaggregated during collection for performance at query time. 
Dashboarding, realtime alerting  
stored as preaggregated time-series with key dimensions 
SDK can preaggregate before sending

**Custom metrics**  

## Application Map 
view performance across all components  
component are independant deployable parts 
differ from observed external dependencies like SQL, Event hubs 
can be spread across App Insights and Subscriptions 
Follows http dependancy calls across servers with App Insights SDK installed  
**Update Map** refreshes components (useful when spread across App Insights ) 
The **cloud role name** can be set/overrided