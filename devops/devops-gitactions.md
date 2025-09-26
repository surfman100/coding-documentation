# GitHub Actions

## YAML Files  
Store in solution root under .github\workflows

### Linux Web Application
```
# This workflow will build and push a .NET Core app to an Azure Web App when a commit is pushed to your default branch.
#
# This workflow assumes you have already created the target Azure App Service web app.
# For instructions see https://docs.microsoft.com/en-us/azure/app-service/quickstart-dotnetcore?tabs=net60&pivots=development-environment-vscode
#
# To configure this workflow:
#
# 1. Download the Publish Profile for your Azure Web App. You can download this file from the Overview page of your Web App in the Azure Portal.
#    For more information: https://docs.microsoft.com/en-us/azure/app-service/deploy-github-actions?tabs=applevel#generate-deployment-credentials
#
# 2. Create a secret in your repository named AZURE_WEBAPP_PUBLISH_PROFILE, paste the publish profile contents as the value of the secret.
#    For instructions on obtaining the publish profile see: https://docs.microsoft.com/azure/app-service/deploy-github-actions#configure-the-github-secret
#
# 3. Change the value for the AZURE_WEBAPP_NAME. Optionally, change the AZURE_WEBAPP_PACKAGE_PATH and DOTNET_VERSION environment variables below.
#
# For more information on GitHub Actions for Azure: https://github.com/Azure/Actions
# For more information on the Azure Web Apps Deploy action: https://github.com/Azure/webapps-deploy
# For more samples to get started with GitHub Action workflows to deploy to Azure: https://github.com/Azure/actions-workflow-samples

name: Deploy [develop] branch to Dev

env:
  AZURE_WEBAPP_NAME: app-customerstatement-dev    # set this to the name of your Azure Web App
  AZURE_FUNCTIONAPP_NAME: func-customerstatement-dev
  AZURE_WEBAPP_PACKAGE_PATH: '.'      # set this to the path to your web app project, defaults to the repository root
  AZURE_FUNCTIONAPP_PACKAGE_PATH: '.'       # set this to the path to your function app project, defaults to the repository root
  DOTNET_VERSION: '8.0'                 # set this to the .NET Core version to use

on:
  push:
    branches: [ "develop" ]
  workflow_dispatch:

permissions:
  id-token: write
  contents: read

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v3

      - name: Set up .NET Core
        uses: actions/setup-dotnet@v2
        with:
          dotnet-version: ${{ env.DOTNET_VERSION }}

      - name: Set up dependency caching for faster builds
        uses: actions/cache@v3
        with:
          path: ~/.nuget/packages
          key: ${{ runner.os }}-nuget-${{ hashFiles('**/packages.lock.json') }}
          restore-keys: |
            ${{ runner.os }}-nuget-

      - name: Build Web Project
        run: dotnet build src/CustomerStatement.Web/CustomerStatement.Web.csproj --configuration Release

      - name: Publish Web Project
        run: dotnet publish src/CustomerStatement.Web/CustomerStatement.Web.csproj -c Release -o ${{env.DOTNET_ROOT}}/myapp

      - name: Upload Web Project artifact for deployment job
        uses: actions/upload-artifact@v4
        with:
          name: .net-app-${{ matrix.runs-on }}
          path: ${{env.DOTNET_ROOT}}/myapp

      - name: Build Function Project
        shell: bash
        run: |
          pushd './${{ env.AZURE_FUNCTIONAPP_PACKAGE_PATH }}'
          dotnet build src/CustomerStatement.Functions/CustomerStatement.Functions.csproj  --configuration Release --output ${{env.DOTNET_ROOT}}/output
          popd

      - name: Upload Function Project artifact for deployment job
        uses: actions/upload-artifact@v4
        with:
          name: .function-app-${{ matrix.runs-on }}
          path: ${{env.DOTNET_ROOT}}/output
            

  deployweb:
    permissions:
      contents: none
    runs-on: ubuntu-latest
    needs: build
    environment:
      name: 'Dev'
      url: ${{ steps.deploy-to-webapp.outputs.webapp-url }}

    steps:
      - name: Download artifact from build job
        uses: actions/download-artifact@v4
        with:
          name: .net-app-${{ matrix.runs-on }}

      - name: Deploy to Azure Web App
        id: deploy-to-webapp
        uses: azure/webapps-deploy@v2
        with:
          app-name: ${{ env.AZURE_WEBAPP_NAME }}
          publish-profile: ${{ secrets.AZURE_WEBAPP_PUBLISH_PROFILE_DEV }}
          package: ${{ env.AZURE_WEBAPP_PACKAGE_PATH }}
  
  deployfunction:
    permissions:
      contents: none
    runs-on: ubuntu-latest
    needs: build
    environment:
      name: 'Dev'
      url: ${{ steps.deploy-to-webapp.outputs.webapp-url }}

    steps:
      - name: Download artifact from build job
        uses: actions/download-artifact@v4
        with:
          name: .function-app-${{ matrix.runs-on }}

      - name: Run Azure Functions Action
        uses: Azure/functions-action@v1
        id: fa
        with:
          app-name: ${{ env.AZURE_FUNCTIONAPP_NAME }}
          package: '${{ env.AZURE_FUNCTIONAPP_PACKAGE_PATH }}'
          publish-profile: ${{ secrets.AZURE_FUNCTIONAPP_PUBLISH_PROFILE_DEV }}

```