# Azure Log Analytics

![image](https://github.com/user-attachments/assets/2a6d0a0d-8d37-40ed-9d5a-15c3c1df4464)


## Overview
- Create a Workspace. This is the storage mechanism in Azure Monitor
  - Container for logs
  - Allows management of logs
  - Allows for exploration of logs 
- Made up of tables with different columns
- Many different data sources feed this and spread the data across these tables
- These data can then be used by many different end applications
   - App Insights
   - Log Queries
   - Alerts
   - etc
- Logs are resource centric. Clicking logs on a Resource (eg App Service....or could use a Resource Group!)  will show relevant logs even if these span workspaces

## Types
- Metrics: stored in time series database
- 

## Tables
- 6 default tables create for any use - alert, usage etc
- interactive retention (6-90 days) and restore retention (7 years)
- two plan types analytics v basic
- you can add Custom columns or Custom tables
   - suffixes will be appended
- you can create transformations
   - hide columns, modify etc

