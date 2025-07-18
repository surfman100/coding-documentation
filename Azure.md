# Azure
General concepts, hints and tips.

## Table of Contents
1. [App Registrations](#appregistrations)
2. [Service Principals](#ServicePrincipals)
3. [Enterprise Applications](#EnterpriseApplications)
4. [Web App](#WebApp)
5. [App Configuration](#AppConfiguration)
6. [Key Vault and App Configuration](#KeyVaultandAppConfiguration)
7. [Secrets Manager](#SecretsManager)

## Applications

<a name="appregistrations" />

### App Registrations
- Use App Registration to register *your* application for use with Entra i.e. Identity
- for identity provider to know that a user has access to an app, the user and the app must be registered
- Is an abstract entity, global representation
- Also allows us:
  -  to brand the sign-on experience, control what users have access
  - The app can request scope permissions e.g. "User.Read" to read the user profile
  - Share a secret with Identifity platform which *proves the apps identity*. (used as our app is confidential). Uses this secret when requesting tokens.

<a name="ServicePrincipals" />

### Service Principals
- Local representation of global application in a specific tenant
- Service principals are a Microsoft Entra application resource you create within your tenant to perform unattended resource and service level operations.
- They're a unique type of user identity with an application ID and password or certificate.
- A service principal has only those permissions necessary to perform tasks defined by the roles and permissions for which it is assigned. (defines what an application can do in a tenant)

<a name="EnterpriseApplications" />

### Enterprise Applications
- Use these to register an instance of this application. Other organisations could have an Enterprise Application for your App Registration.
- You'll see many Enterprise applications listed as this will contain those which are used by your organisation but built but others (e.g. Adobe etc)
- The enterprise application resource controls what the app can do in our tenant

<a name="WebApp" />

### Managed Identity
- Special type of Service Principal that eliminates the need to manage credentials


### Web App
- create a web application (does not need an App Registration etc)
- push code to this using GIT. This is a great option, can set this for CI.
- note the use of logs under *App Service Logs*
- Git Workflow:
  - Actions builds the projects
  - Deployments can be seen under Environments
  - The configuration files are saved has .yml with the code
- Alternative to pushing code to GITHub and then using Worflow is:
  - push code directly to Web App
  - there is an automatic build under Deployment area [Oryx](https://github.com/microsoft/Oryx/tree/main)
  - setup your deployment/git options if need be 

<a name="AppConfiguration" />

### App Configuration
the simplest app configuration is just to use the "Configuration" tab in a Wep App blade.

alternative is to use the fully featured App Configuration service.
- add using the portal
- save the connection string to secrets manager and add reference using:
 ```
dotnet user-secrets init
dotnet user-secrets set ConnectionStrings:AppCondig "<url here>"
dotnet add package Microsoft.Azure.AppConfiguration.AspNetCore
```
- remember to use this on server you'll need to add the AppConfig endpoint under the App Settings, Connection string area

in the VS project
- add a model for the Settings
- read the connection string, load configuration, add bind to model
```
// Retrieve the connection string
string connectionString = builder.Configuration.GetConnectionString("AppConfig");

// Load configuration from Azure App Configuration
builder.Configuration.AddAzureAppConfiguration(connectionString);

// Bind configuration "TestApp:Settings" section to the Settings object
```

<a name="KeyVaultandAppConfiguration" />

### Key Vault and App Configuration
#### code
Add the option for Key Vault Reference retrieval
```
builder.Configuration.AddAzureAppConfiguration(options =>
{
    options.Connect(builder.Configuration.GetConnectionString("AppConfigEndPoint"));

    options.ConfigureKeyVault(kv =>
    {
        kv.SetCredential(new DefaultAzureCredential());
    });
});
```

### local development
The default credential tries using one of a number of credentials to connect. 
To Use the first, EnvironmentCredential, add the environment variables in **launch.settings.json** (and not launch.json! Also note it should be under the launch profile that you are using)
```
        "AZURE_TENANT_ID":"<guid>",
        "AZURE_CLIENT_ID":"<guid>",
        "AZURE_CLIENT_SECRET":"<guid>"
```
On the Key Vault IAM, Add the Service Principal as a * *Key Vault Secrets User* *. 

#### server side
For this to work, you need to enable the managed identity on the App Service and grant this managed identity the same * *Key Vault Secrets User* * role

<a name="Secrets Manager" />

### Secrets Manager
- use the secrets manager to save secrets in development environment to local json file

### Script to create basic App Service
```
az group create --name myResourceGroup --location "West Europe"
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1 --is-linux
az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name "BillAzureMonitorTestDebug" --runtime "PHP|8.1" --deployment-local-git
az webapp config appsettings set --name "BillAzureMonitorTestDebug" --resource-group myResourceGroup --settings DEPLOYMENT_BRANCH='main'
git clone https://github.com/Azure-Samples/App-Service-Troubleshoot-Azure-Monitor
cd App-Service-Troubleshoot-Azure-Monitor
git branch -m main
git remote add azure https://bill.tierney2@billazuremonitortestdebug.scm.azurewebsites.net/BillAzureMonitorTestDebug.git
git push azure main
```
