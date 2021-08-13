# GitHub Actions

This repo is collection of different GitHub Actions.

## Azure PowerShell action

You can use this GitHub action for executing Azure PowerShell in your own GitHub workflows.
Similarly as [Azure PowerShell task](https://docs.microsoft.com/en-us/azure/devops/pipelines/tasks/deploy/azure-powershell?view=azure-devops) in
Azure DevOps.

Primary use case is to call ARM template deployments using `deploy.ps1` (deployment entrypoint)
to make your template deployments easy but you can of course use this for
any Azure automation scenarios you might on your mind.

Read more about it in [this blog post](https://dev.to/janne_mattila/azure-powershell-and-arm-template-deployment-from-github-actions-2038). 

### Example

Here's small [example](https://github.com/JanneMattila/AzurePwshARMActionDemo/blob/master/.github/workflows/main.yml) how to execute Azure PowerShell in your own workflow:

```yaml
name: Azure Deployment example
on: [push]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v1

    - uses: jannemattila/actions/azurepowershell@master
      with:
        creds: ${{ secrets.AZURE_CREDENTIALS }}
        
    - name: Azure PowerShell & ARM template deployment
      run: ./deploy/deploy.ps1 -ResourceGroupName "pwsh-dev-rg" -Location "North Europe"
      shell: pwsh
```

In this example you first checkout your codebase and then execute `/deploy/deploy.ps1`
PowerShell script to deploy your ARM template ([example](https://github.com/JanneMattila/AzurePwshARMActionDemo/blob/master/deploy/deploy.ps1)). 

You can find example project in [here](https://github.com/JanneMattila/AzurePwshARMActionDemo).
