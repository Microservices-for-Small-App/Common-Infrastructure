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
$rg-name="rg-womd-robbie-001"
az group create --name $rg-name --location eastus
```

## Creating the Cosmos DB account

```powershell
az cosmosdb create --name cosmosdb-playeconomy --resource-group $rg-name --kind MongoDB --enable-free-tier
```

## Creating the Service Bus namespace

```powershell
az servicebus namespace create --name sb-playeconomy --resource-group $rg-name --sku Standard 
```

## Creating the Container Registry

```powershell
az acr create --name acr-playeconomy --resource-group $rg-name --sku Basic
```
