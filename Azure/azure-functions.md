# Azure Functions
Need to understand the nuances and differences compared to a simple C# Class Library

## Hosting Options 

| Option | Description | Scale Out | 
| --- | --- | --- |
| Consumption | default. pay as you go. | event driven | 
| Flex Consumption | configure instances. High scalability. | function based |
| Premium | prewarmed workers, powerful instances, vnets connectivity, CPU intensive | event driven 
| Dedicated | full isolation, predicatable billing, high mem | manual/autoscale |
| Container Apps | hosted by Azure Container Apps, custom libs | event driven |

## Files 

| File | Description |
| --- | --- | 
| host.json | every language. config options. binding configs applied to all | 
| local.settings.json | every language. local configuration options. | 
| App Settings | cloud configuration settings | 
| function.json |  | 

In development, use connection strings in local.settings.json 

## Bindings / Triggers 

**triggers**: how invoked, 1 only, associated data 
**bindings**: optional. declaratively connecting to other services. input/output. 

| Language | Configure by... |
| --- | --- | 
| c# | decorating methods/parameters c# attributes  | 
| java | decorating methods/parameters c# annotations  | 
| scripts | updating functions.json  | 

Azure Files doesn't support using managed identity when accessing the file share

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
```
//in the configuration of the EF context, enable this option
  services.AddDbContext<MyContext>(options => options.UseSqlServer(hostContext.Configuration["ConnString"], options=>options.EnableRetryOnFailure()));

```

## Functions v WebJobs   
Webjobs more limited 
