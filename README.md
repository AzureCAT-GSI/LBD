# LBD
## Library Based Deployment repository

This library is intended to host an Azure template solution that contains basic templates to be referenced on more complex template solutions, the concept is similar to Azure Building Blocks (https://github.com/mspnp/template-building-blocks/wiki) but for more basic operations, like create virtual machines, change ip addresses from dynamic to static, assign DNS to a virtual network or to a virtual machine, etc. Azure Building Blocks goes beyond this and achieves more complex scenarios with less code through parameter files.

LBD is meant for those who still wants to simplify its resource manager templates and keep the same look and feel and full control of a template.

## Getting started

1) Create a deployment solution with Visual Studio 2017
2) When consuming templates from this solution we need to provide a unique string every time we perform a deployment, so troubleshooting gets easier and we avoid issues of deployment names already there. Replace the default VS 2017 Depployment script Deploy-AzureResourceGroup.ps1 with the one provided in this solution, located at https://raw.githubusercontent.com/AzureCAT-GSI/LBD/master/LibraryBasedDeployment/LBD/Deploy-AzureResourceGroup.ps1.
3) Use the template file \_scenario_template.json located at https://raw.githubusercontent.com/AzureCAT-GSI/LBD/master/LibraryBasedDeployment/LBD/Scenarios/_scenario_template.json as your starting point since this template of template contain the URLs for all library items you can use plus a base deployment resource where the only optional parameter is the sasToken. 

## Examples

There are three deployment examples in this solution and they can be found at https://github.com/AzureCAT-GSI/LBD/tree/master/LibraryBasedDeployment/LBD/Scenarios.

## Test Cases

For more indiviual examples on how to use the library items, there is a TestCase.json template that contains multiple exemples on how to use each item. It can be found at https://github.com/AzureCAT-GSI/LBD/tree/master/LibraryBasedDeployment/LBD/TestCases. When contributing to expanding this library, we need to add new test cases to include all possible usages of the new item.