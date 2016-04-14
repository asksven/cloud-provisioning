# Deploy an Azure Website using the Azure CLI

This is a simple deployment of an Azure website (Paas) based on ARM and the Azure CLI. 

## About the Azure CLI

The doc about using the Azure CLI can be found here: https://github.com/Azure/azure-content/blob/master/articles/xplat-cli-azure-resource-manager.md

## Project overview

- azuredeploy.json is the ARM template defining the resource (based on this one https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json)
- azuredeploy.parameters.json is the file containing the parameters for a specific environment. This file is passed as parameter when building the resource
- REAME.md is this file

## Usage

### TLDR;

Click here and you will be taken to the portal to enter the parameters (requires a mouse).

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png"/>
</a>
<a href="http://armviz.io/#/?load=https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json" target="_blank">
    <img src="http://armviz.io/visualizebutton.png"/>
</a>

### TLDR; (is you have a console and what to learn something)

    azure config more arm
    azure group create my-first-web-app-rg westeurope
    azure group deployment create my-first-web-app-rg my-first-web-app -f azuredeploy.json
    
Just click here:     

### Pre-Requisite

The Azure CLI must be installed:
    azure -version

should echo something like this:
    0.9.19 (node: 5.10.1)    

### Use the CLI in arm-mode

The CLCI supports both "classic" and "arm" mode. Before deploying an ARM template we need to explicitely tell the CLI to use the arm-mode

    azure config mode arm

The mode does not need to be set for each execution. Whether the CLI is already configured for ARM can be looked up by entering

    azure config list

### Log-in to Azure

Execute following command and follow the workflow:

    azure login
    
### Note if your user has multiple subscriptions

Before running any command you should verify that you are on the right subscription. The available as well as the current (default) subscription can be listed with following command:
 
    azure account list
    
From the list make sure that the subscription you intend to deploy the resource to is the one marked as ``true`` in the column ``current``.

### Resource group

ARM resources are deployed to resource groups. Available resource groups can be listed with

    azure group list
    
and a new resource group can be create with 

    azure group create <name> <location>
    
Where ``<location>`` is a valid Azure location. The list of locations can be obtained by executing

    azure location list
    
Let's create a resource group called ``my-first-web-app`` located in west europe:

    azure group create my-first-web-app-rg westeurope            
### Interactive creation of the resource

#### Validate your template

    azure group template validate -f ./azuredeploy.json -g my-first-web-app-rg
    
will take you through the parameters and validate the entry / template.

    $ azure group template validate -f ./azuredeploy.json -g my-first-web-app-rg
    info:    Executing command group template validate
    info:    Supply values for the following parameters
    siteName: my-first-web-app
    hostingPlanName: free
    siteLocation: westeurope
    + Initializing template configurations and parameters                          
    + Validating the template                                                      
    info:    group template validate command OK

#### Create your resource
    
With interactive we mean that the resource is being created without parmeter-file. All parameters of the ARM template will be entered on the console.

    azure group deployment create my-first-web-app-rg my-first-web-app -f azuredeploy.json        
    
### Non-interactive creation of the resource

Same as above buy adding the ``-p <param-file>`` argument
    
Beware: the CLI seems to have trouble with parsing param-files at this moment. 
TODO