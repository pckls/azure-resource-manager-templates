# property-transformer-and-collector

I've tested that this works using Azure CLI.

```
$ az group deployment create \
--name DemoNSGDeploy \
--mode Incremental \
--resource-group DemoNSG \
--template-file azureDeploy.json \
--parameters azureDeploy.parameters.json
{
  "id": "/subscriptions/<subscription-id>/resourceGroups/DemoNSG/providers/Microsoft.Resources/deployments/DemoNSGDeploy",
  "name": "DemoNSGDeploy",
  "properties": {
    "correlationId": "<correlation-id>",
    "debugSetting": null,
    "dependencies": [
      {
        "dependsOn": [
          {
            "id": "/subscriptions/<subscription-id>/resourceGroups/DemoNSG/providers/Microsoft.Resources/deployments/collector",
            "resourceGroup": "DemoNSG",
            "resourceName": "collector",
            "resourceType": "Microsoft.Resources/deployments"
          }
        ],
        "id": "/subscriptions/<subscription-id>/resourceGroups/DemoNSG/providers/Microsoft.Network/networkSecurityGroups/networkSecurityGroup1",
        "resourceGroup": "DemoNSG",
        "resourceName": "networkSecurityGroup1",
        "resourceType": "Microsoft.Network/networkSecurityGroups"
      }
    ],
    "mode": "Incremental",
    "outputs": {
      "instance": {
        "type": "Array",
        "value": [
          {
            "name": "RDPAllow",
            "properties": {
              "access": "Allow",
              "description": "allow RDP connections",
              "destinationAddressPrefix": "10.0.0.0/24",
              "destinationPortRange": "3389",
              "direction": "Inbound",
              "priority": 100,
              "protocol": "Tcp",
              "sourceAddressPrefix": "*",
              "sourcePortRange": "*"
            }
          },
          {
            "name": "HTTPAllow",
            "properties": {
              "access": "Allow",
              "description": "allow HTTP connections",
              "destinationAddressPrefix": "10.0.1.0/24",
              "destinationPortRange": "80",
              "direction": "Inbound",
              "priority": 200,
              "protocol": "Tcp",
              "sourceAddressPrefix": "*",
              "sourcePortRange": "*"
            }
          }
        ]
      }
    },
    "parameters": {
      "collectorTemplateUri": {
        "type": "String",
        "value": "https://raw.githubusercontent.com/pckls/azure-resource-manager-templates/master/property-transformer-and-collector/Resources/networkSecurityGroups/collector.json"
      },
      "networkSecurityGroupsSettings": {
        "type": "Object",
        "value": {
          "securityRules": [
            {
              "access": "Allow",
              "description": "allow RDP connections",
              "destinationAddressPrefix": "10.0.0.0/24",
              "destinationPortRange": "3389",
              "direction": "Inbound",
              "name": "RDPAllow",
              "priority": 100,
              "protocol": "Tcp",
              "sourceAddressPrefix": "*",
              "sourcePortRange": "*"
            },
            {
              "access": "Allow",
              "description": "allow HTTP connections",
              "destinationAddressPrefix": "10.0.1.0/24",
              "destinationPortRange": "80",
              "direction": "Inbound",
              "name": "HTTPAllow",
              "priority": 200,
              "protocol": "Tcp",
              "sourceAddressPrefix": "*",
              "sourcePortRange": "*"
            }
          ]
        }
      },
      "transformTemplateUri": {
        "type": "String",
        "value": "https://raw.githubusercontent.com/pckls/azure-resource-manager-templates/master/property-transformer-and-collector/Resources/networkSecurityGroups/transform.json"
      }
    },
    "parametersLink": null,
    "providers": [
      {
        "id": null,
        "namespace": "Microsoft.Resources",
        "registrationState": null,
        "resourceTypes": [
          {
            "aliases": null,
            "apiVersions": null,
            "locations": [
              null
            ],
            "properties": null,
            "resourceType": "deployments"
          }
        ]
      },
      {
        "id": null,
        "namespace": "Microsoft.Network",
        "registrationState": null,
        "resourceTypes": [
          {
            "aliases": null,
            "apiVersions": null,
            "locations": [
              "southeastasia"
            ],
            "properties": null,
            "resourceType": "networkSecurityGroups"
          }
        ]
      }
    ],
    "provisioningState": "Succeeded",
    "template": null,
    "templateLink": null,
    "timestamp": "2017-12-20T07:11:44.133501+00:00"
  },
  "resourceGroup": "DemoNSG"
}
$
```
