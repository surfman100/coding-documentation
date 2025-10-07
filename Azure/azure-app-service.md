# Azure App Service
General tips
- When using App Config, ensure you have the connection string in the Environment App Settings!
- If encountering problems, check the Logs to ensure the service actually started without errors

## Plan Types

| Plan | VM Type |
| --- | --- |
| Free | A |
| Shared | A |
| Basic | A |
| Standard | A |
| Premium | A |
| PremiumV2 | B |
| PremiumV3 | C |

Note that different VM family types have different outbound addresses.

## Container Applications 
Slightly different setup process, point a registry and image 


## API Management
Consists of:  

| Component | Description | 
| --- | --- |
| API Gateway (data plane/runtime) | accepts, routes API calls. Enforce limits, key verification |  
| Management Plane | Provision, Managed Users, package apis into **Products** |
| Developer portal | Documentation www | 

**Permissions**
- Products: Open or Protected  
- Groups: Administrators, Developers, Guests (view not call APIs)  
- Policies: executed on a request/response. inbound, outbound, backend, on-error

Self hosted option exists for multicloud  
subscription keys are the mechanism for securing. Also OAuth2, Client certs, IP allow listing  
key included on each request **Ocp-Apim-Subscription-Key** header   

```
<policies>
    <inbound>
        <base />
        <set-header name="x-request-context-data" exists-action="override">
            <value>@(context.User.Id)</value>
            <value>@(context.Deployment.Region)</value>
      </set-header>
    </inbound>
<outbound>
    <base />
    <choose>
      <when condition="@(context.Response.StatusCode == 200 && context.Product.Name.Equals("Starter"))">
        <!-- NOTE that we are not using preserveContent=true when deserializing response body stream into a JSON object since we don't intend to access it again. See details on /azure/api-management/api-management-transformation-policies#SetBody -->
        <set-body>
          @{
            var response = context.Response.Body.As<JObject>();
            foreach (var key in new [] {"minutely", "hourly", "daily", "flags"}) {
            response.Property (key).Remove ();
           }
          return response.ToString();
          }
    </set-body>
      </when>
    </choose>    
  </outbound>
</policies>

// also  
<forward-request timeout="time in seconds" follow-redirects="true | false"/>
<limit-concurrency key="expression" max-count="number">
<log-to-eventhub logger-id="id of the logger entity" partition-id="...">
<mock-response status-code="code" content-type="media type"/>
```

open api specification?