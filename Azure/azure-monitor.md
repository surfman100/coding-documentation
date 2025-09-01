# Azure Monitor 

![Monitor](/Azure/platform-logs-metrics.png)

## Data Storage

| Type | Description  | Stored |
| --- | --- | --- |
| Metrics | time-series | Stored in Azure Monitor metrics DB |
| Log data | events | Stored in Azure Monitor log storage. Use Log Analytics to query |
| Distributed traces | related events | Use App Insights | 
| Changes | series of events | Change Analysis tool | 
| Azure activity Log | | Seperate Store | 

Both metrics and acitivity can be routed to log storage.
Use diagnositics to route to log storage outside of Azure Monitor. 

Application Insights allow you to look at both types of data without needing to know whether metrics or log data.