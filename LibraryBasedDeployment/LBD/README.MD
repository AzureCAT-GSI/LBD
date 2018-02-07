Notes related to some linked templates in this solution
-------------------------------------------------------

* *changeVmIpAddrTypeOnly.json*
  * When using this template, beware that you need to know exactly how the VM NIC is configured in order to be able to trigger the correct configuration.
  * You tell which optional attributes to include based on how your current NIC is setup, this is done through the parameter called *nicOptionalAttributeSet* and the valid values are:
        
        "all",
        "none",
        "nsg",
        "nsg-pip",
        "nsg-lbBe",
        "nsg-lbBe-lbNat",
        "nsg-LbNat",
        "nsg-pip-lbBe",
        "nsg-pip-lbBe-lbNat",
        "nsg-pip-LbNat",
        "pip",
        "pip-lbBe",
        "pip-lbBe-lbNat",
        "pip-LbNat",
        "lbBe",
        "lbBe-lbNat",
        "LbNat"

Unsupported Scenarios
---------------------

* Multiple NICs with Static Public IP Addresses
* Change VM Ip Address from Dynamic to Static after VM is deployed when the VM has multiple IP Configurations (it works now only when VM has one IpConfiguration, it also works with multiple NICs, Ip Configuration 1 of all NICs will be converted to Static using the current IP Address)


Snippets
--------

Getting the value of a section that was created using the copy attribute: 

```
  "outputs": {
    "allNatRules": {
      "type": "object",
      "value": "[variables('lb2natRules')]"
    },
    "nat1": {
      "type": "string",
      "value": "[concat(resourceid('Microsoft.Network/loadBalancers',variables('lb2Name')), '/inboundNatRules/',variables('lb2natRules').lb2natCopy[0].name)]"
    }
  }
```

Getting reference for an object:

1. Execute the getReference.json template to get the reference as follows:
```
   {
      "condition": true,
      "comments": "Getting a reference for a vnet",
      "name": "[concat(variables('deploymentUniqueString'),'-','getVnetRef')]",
      "type": "Microsoft.Resources/deployments",
      "apiVersion": "2017-05-10",
      "dependsOn": [
        "[concat('Microsoft.Resources/deployments/',variables('deploymentUniqueString'),'-',variables('vnetName'),'vNetDeployment-TestCase1')]"
      ],
      "properties": {
        "mode": "Incremental",
        "templateLink": {
          "uri": "[variables('getRefUri')]",
          "contentVersion": "1.0.0.0"
        },
        "parameters": {
          "deploymentUniqueString": {
            "value": "[variables('deploymentUniqueString')]"
          },
          "sasToken": {
            "value": "[parameters('_artifactsLocationSasToken')]"
          },
          "resourceId": {
            "value": "[resourceId('Microsoft.Network/virtualNetworks',variables('vnet1Name'))]"
          },
          "apiVersion": {
            "value": "2017-06-01"
          }
        }
      }
    }
```

2. Consume the returned values as follows:

```
    "outputs": {
        "resourceObj": {
          "type": "object",
          "value": "[reference(concat(variables('deploymentUniqueString'),'-','getVnetRef')).outputs.resourceObj]"
        },
        "fullResourceObj": {
          "type": "object",
          "value": "[reference(concat(variables('deploymentUniqueString'),'-','getVnetRef')).outputs.fullResourceObj]"
        }
```

3. 
