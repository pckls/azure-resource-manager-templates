# resource-group-creation

Azure/azure-docs-json-samples#58

Referencing the existing template with my changes I'm able to loop over an object of resource groups and create them.

```
C:\Users\pckls\Code\azure-resource-manager-templates\resource-group-creation [master ≡]
λ  New-AzureRmDeployment -Location westus -TemplateFile .\azureDeploy.json -TemplateParameterFile .\azureDeploy.parameters.json


DeploymentName          : azureDeploy
Location                : westus
ProvisioningState       : Succeeded
Timestamp               : 14/11/2018 7:55:49 AM
Mode                    : Incremental
TemplateLink            :
Parameters              :
                          Name             Type                       Value
                          ===============  =========================  ==========
                          resourceGroups   Array                      [
                            {
                              "name": "myrg-eastus",
                              "location": "eastus",
                              "tags": {
                                "hello": "world"
                              }
                            },
                            {
                              "name": "myrg-westus",
                              "location": "westus",
                              "tags": {
                                "foo": "bar"
                              }
                            }
                          ]

Outputs                 :
DeploymentDebugLogLevel :

C:\Users\pckls\Code\azure-resource-manager-templates\resource-group-creation [master ≡]
λ
```