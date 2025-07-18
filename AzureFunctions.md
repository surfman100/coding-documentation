# Azure Functions
Need to understand the nuances and differences compared to a simple C# Class Library

## Deployment issues
Sometimes if you can't see the list of function methods when you deploy via git actions.

This helped:
1. Deploy from command line
```
func azure functionapp publish func-customerstatement-prod --dotnet-version 8.0 -c release
```

2. Set this setting
```
az functionapp config appsettings set --name func-customerstatement-prod -g rg-reporting-prod --settings SCM_DO_BUILD_DURING_DEPLOYMENT=true
```
