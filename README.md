# Devops-Terraform-1July
# Starter pipeline
# Start with a minimal pipeline that you can customize to build and deploy your code.
# Add steps that build, run tests, deploy, and more:
# https://aka.ms/yaml

trigger:
- main

pool:
  name: 'terraform agent'

steps:
- task: TerraformInstaller@1
  inputs:
    terraformVersion: 'latest'


- task: TerraformTask@5
  inputs:
    provider: 'azurerm'
    command: 'init'
    backendServiceArm: 'tfconnection'
    backendAzureRmResourceGroupName: 'tfrg'
    backendAzureRmStorageAccountName: 'tfstroage505'
    backendAzureRmContainerName: 'tfcontainer'
    backendAzureRmKey: 'tfkey'
- task: TerraformTask@5
  inputs:
    provider: 'azurerm'
    command: 'plan'
    environmentServiceNameAzureRM: 'tfconnection'
- task: TerraformTask@5
  inputs:
    provider: 'azurerm'
    command: 'apply'
    environmentServiceNameAzureRM: 'tfconnection'
