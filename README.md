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
az cosmosdb create --name cosmosdb-playeconomy --resource-group $rgname --kind MongoDB --enable-free-tier
```

## Creating the Service Bus namespace

```powershell
az servicebus namespace create --name sb-playeconomy --resource-group $rgname --sku Standard 
```

## Creating the Container Registry

```powershell
az acr create --name acrplayeconomydev001 --resource-group $rgname --sku Basic
```
