# Azure DevOps

## Pipeline tasks
- Very important to use the correct task for the activity you are trying to accomplish.
- Be aware of differences in App Service deployment for Linux
  - Watch out for case sensitive files in Linux!!

## Functions Deployment Sample
This sample deploys to Linux App Service
```
trigger:
  batch: true
  branches:
    include:
    - master
  paths:
    include:
    - src/MySolution.Functions/*
    - src/MySolution.BusinessLogic/*

pool:
  vmImage: windows-latest

variables:
  buildConfiguration: 'Release'

steps:
- task: DotNetCoreCLI@2
  displayName: Publish Azure Function
  inputs:
    command: 'publish'
    publishWebProjects: false
    projects: 'src/MySolution.Functions/MySolution_Functions.csproj'
    arguments: '--configuration $(buildConfiguration)  --output publish_output'
    modifyOutputPath: false
    zipAfterPublish: false
# Archive files v2
# Compress files into .7z, .tar.gz, or .zip.
- task: ArchiveFiles@2
  inputs:
    rootFolderOrFile: "$(System.DefaultWorkingDirectory)/publish_output"
    includeRootFolder: false
    archiveType: 'zip'
    archiveFile: '$(System.DefaultWorkingDirectory)/build$(Build.BuildId).zip'
- task: PublishBuildArtifacts@1
  displayName: "Publish Artifacts"
  inputs:
    PathtoPublish: '$(System.DefaultWorkingDirectory)/build$(Build.BuildId).zip'
    artifactName: 'drop'
-  task: DownloadBuildArtifacts@1 # Add this at the end of your file
   inputs:
    buildType: 'current'
    downloadType: 'single'
    artifactName: 'drop'
    itemPattern: '**/*.zip'
    downloadPath: '$(System.ArtifactsDirectory)'
- task: AzureFunctionApp@2
  displayName: Deploy Azure Function
  inputs:
    connectedServiceNameARM: mysolution-prod
    appType: 'functionAppLinux'
    appName: func-mysolution-prod
    resourceGroupName: rg-mysolution-prod
    package: '$(System.ArtifactsDirectory)/**/*.zip'
    runtimeStack: 'DOTNET-ISOLATED|9.0'
    deploymentMethod: 'zipDeploy'
