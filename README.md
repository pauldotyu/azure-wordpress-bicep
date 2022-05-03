# azure-wordpress-bicep

This WordPress on App Service deployment is based on the recent announcement of a ["New and better 'WordPress on App Service'"](https://techcommunity.microsoft.com/t5/apps-on-azure-blog/the-new-and-better-wordpress-on-app-service/ba-p/3202594).

To deploy this template, you will need the following:

1. Git to clone this repo
1. Azure Subscription
1. [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
1. [Azure Bicep](https://docs.microsoft.com/en-us/azure/azure-resource-manager/bicep/install)

Using your favorite terminal, run the folowing commands to deploy:

> NOTE: Examples below have been tested in WSL.

```bash
# setup parameters
location="<LOCATION>"
projectName="<GLOBALLY_UNIQUE_NAME>"
username="<USERNAME>"
password="<PASSWORD>"
email="<EMAIL>"

# review the rest of the parameter values in the parameters.json file and override the values

# create a resource group
az group create --name $projectName-rg --location $location

# deploy your bicep file
az deployment group create \
 --name $projectName-deployment \
 --resource-group $projectName-rg \
 --template-file ./main.bicep \
 --parameters @parameters.json \
 --parameters location=$location projectName=$projectName mySqlServerUsername=$username mySqlServerPassword=$password wordpressAdminEmail=$email wordpressUsername=$username wordpressPassword=$password
```

To destroy your resources, run the following command:

```bash
az group delete -n $projectName-rg -y
```
