# Deploy Azure Function App with Private Storage

## Overview

This ARM Template deploys the following:

- App Service Plan
- Function App (with VNet Integration to secure Outbound traffic)
- Function App Private Endpoint (for inbound access to the App)
- Application Insights
- Subnet Delegation for Microsoft.Web/serverFarms
- Storage Account
- Storage Account Blob Private Endpoint
- Private Endpoint Private DNS Zone integration

This deployment assumes the following prerequisites are met:

- Existing ResourceGroup to be used for the Function App, App Service Plan, Storage Account, App Insights, and Private Endpoint.
- Existing Virtual Network that will be used for the Function App VNet integration and the Storage Account Private Endpoint.
- Existing Function App and Private Endpoint subnets
- Existing Private DNS zone for ```privatelink.blob.core.windows.net```

## Usage

1. Open ```functionAppDeploy.json``` and edit the ```DefaultValue``` for ```privateDnsZoneSubscription``` and ```privateDnsZoneResourceGroup```. These will be hardcoded.

2. Open ```functionAppDeploy.parameters.json``` and update the parameters.

3. Save both files.

4. Deploy using the ResourceGroup deployment method targeting the Function App Resource Group. If the Function App RG is **RG-FunctionApp** then the deployment in PowerShell will look like this:

```PowerShell
new-azresourcegroupdeployment -ResourceGroupName "RG-FunctionApp" -name "FuncAppTestDeployment" -TemplateFile functionAppDeploy.json -TemplateParameterFile functionAppDeploy.parameters.json
```
