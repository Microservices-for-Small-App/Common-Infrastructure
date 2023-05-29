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

## Installing Emissary-ingress

```powershell
helm repo add datawire https://app.getambassador.io
helm repo list
helm repo update

kubectl apply -f https://app.getambassador.io/yaml/emissary/3.3.0/emissary-crds.yaml
kubectl wait --timeout=90s --for=condition=available deployment emissary-apiext -n emissary-system

$appname="apig-playeconomy-dev-001"
$namespace="emissary"
helm install emissary-ingress datawire/emissary-ingress --set service.annotations."service\.beta\.kubernetes\.io/azure-dns-label-name"=$appname -n $namespace --create-namespace 

helm list -n $namespace

kubectl rollout status deployment/emissary-ingress -n $namespace -w

kubectl get svc emissary-ingress -n $namespace

On GKE/Azure:
  export SERVICE_IP=$(kubectl get svc --namespace emissary emissary-ingress -o jsonpath='{.status.loadBalancer.ingress[0].ip}')

  On AWS:
  export SERVICE_IP=$(kubectl get svc --namespace emissary emissary-ingress -o jsonpath='{.status.loadBalancer.ingress[0].hostname}')

  echo http://$SERVICE_IP:
```
