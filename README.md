# Common-Infrastructure

A Repository to hold Common Infrastructure

## Docker Compose Commands

```dockercompose
docker-compose up -d
```

## Add the GitHub package source

```powershell
$owner="Microservices-for-Small-App"
$username="vishipayyallore"
$gh_pat="[PAT HERE]"

dotnet nuget add source --username $username --password $gh_pat --store-password-in-clear-text --name gHmicroservices "https://nuget.pkg.github.com/$owner/index.json"

dotnet nuget list source
dotnet nuget remove source github
```

## Creating the Azure resource group

```powershell
$rgname="rg-playeconomy-dev-001"
az group create --name $rgname --location eastus
```

## Creating the Cosmos DB account

```powershell
$cosmosdbname="cosmosdb-playeconomy"
az cosmosdb create --name $cosmosdbname --resource-group $rgname --kind MongoDB --enable-free-tier
```

## Creating the Service Bus namespace

```powershell
$sbname="sb-playeconomy"
az servicebus namespace create --name $sbname --resource-group $rgname --sku Standard 
```

## Creating the Container Registry

```powershell
$acrname="acrplayeconomydev001"
az acr create --name $acrname --resource-group $rgname --sku Basic
```

## Creating the Azure Key Vault

```powershell
$kvname="kv-playeconomy-dev-001"
az keyvault create -n $kvname -g $rgname
```
