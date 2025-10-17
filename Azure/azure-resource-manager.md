# Azure Resource Manager
Azure Resource Manager is the deployment and management service for Azure.  
To query Azure resources, like DataFactory pipeline runs, use the Azure Resource Manager  

## Code
Reference the following libraries
```
    <PackageReference Include="Azure.ResourceManager" Version="1.13.1" />
    <PackageReference Include="Azure.ResourceManager.DataFactory" Version="1.8.0" />
```

Include the libraries
```
using Azure.ResourceManager.DataFactory;
using Azure.ResourceManager.DataFactory.Models;
using Azure.ResourceManager;
```

create a client and query the DataFactory
```
    var _armClient = new ArmClient(new DefaultAzureCredential());

    var dataFactory = _armClient.GetDataFactoryResource(new ResourceIdentifier($"/subscriptions/{_subscriptionId}/resourceGroups/{_resourceGroupName}/providers/Microsoft.DataFactory/factories/{_dataFactoryName}"));

    await foreach (DataFactoryPipelineRunInfo pipelineRun in dataFactory.GetPipelineRunsAsync(new RunFilterContent(
        DateTimeOffset.UtcNow.AddDays(-7),
        DateTimeOffset.UtcNow
    )))
    {
        pipelineRuns.Add(new PipelineRunInfo
        {
            PipelineName = pipelineRun.PipelineName,
            RunId = pipelineRun.RunId,
            Status = pipelineRun.Status,
            RunStart = pipelineRun.RunStartOn,
            RunEnd = pipelineRun.RunEndOn
        });
    }

    return pipelineRuns;
}

```