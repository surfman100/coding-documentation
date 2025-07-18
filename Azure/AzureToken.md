# Azure Tokens

## Flow Types

|     | Authorization Code Flow | Client Credentials Flow |
| --- | --- | --- |
| Use Case | User | Service running without interaction |
| Authorization | Uses app / browser | Uses client secret |


## Client Credentials Flow to access Graph API
1. Setup an RBAC Service Principal
```
az login
az ad sp create-for-rbac

{
  "appId": "544a6c9a-8276-44b5-8a7b-a45b6fb39b11",
  "displayName": "azure-cli-2024-08-27-10-43-00",
  "password": "<secret value>",
  "tenant": "aef7d964-ee79-491b-b95e-ebf0e1b9db8c"
}
```
This creates a Service Principle object and and a backing application object

2. Request an Access Token
The following is a Postman prescript
```
let tokenUrl = "https://login.microsoftonline.com/" + pm.collectionVariables.get("tenantId") + '/oauth2/v2.0/token';

const getTokenRequest = {
    method: 'POST',
    url: tokenUrl,
    body: {
        mode: 'formdata',
        formdata: [
            { key: 'grant_type', value: 'client_credentials' },
            { key: 'client_id', value: pm.collectionVariables.get("clientId") },
            { key: 'scope', value: pm.collectionVariables.get("scope") },
            { key: 'client_secret', value: pm.collectionVariables.get("clientSecret") }
        ]
    }
};

pm.sendRequest(getTokenRequest, function (err, res) {
    console.log(err);
    console.log(res);
        pm.collectionVariables.set("bearertoken", res.json().access_token);
});
```
the scope for Graph API is: https://management.azure.com/.default

3. Grant the API permissions to the application
On the Application Registration, grant the necessary API Permissions.
- This might be a Microsoft Graph Application permissions
- Alternatively RBAC permissions might be needed on the resource (eg resource group)

For Client Credentials, ensure that the API permissions has granted User.Read and granted consent for the organisation as per [here](https://www.youtube.com/watch?v=7qt8asY33Aw)

## Authorization Code Flow to access Graph API
Following above:
1. Set the application registration redirect uri to https://localhost
2. Set the grant type to **Authorization Code**
3. Scope is https://graph.microsoft.com/User.Read
