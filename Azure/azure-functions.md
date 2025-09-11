# Azure Functions
Need to understand the nuances and differences compared to a simple C# Class Library

## Failed startup
Its critical that you don't forget App Settings for a successful start up of the Function App.
Typicaly ones include
- AppConfig: for AppConfiguration and KeyVault
- TenantID, ClientID, Secret for correct credentails

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

## build / compatability issues
try:
- updateing function tools to the latest version (use choco)
- be mindful of extension bundles

## service bus
limit the concurrent message processing using
```
    "extensions": {
    "serviceBus": {
      "messageHandlerOptions": {
        "autoComplete": true,
        "maxAutoRenewDuration": "00:05:00",
        "maxConcurrentCalls": 2
      }
    }
```

address transient deadlocks
````
//in the configuration of the EF context, enable this option
  services.AddDbContext<MyContext>(options => options.UseSqlServer(hostContext.Configuration["ConnString"], options=>options.EnableRetryOnFailure()));

```