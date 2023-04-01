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

dotnet nuget add source --username $username --password $gh_pat --store-password-in-clear-text --name github "https://nuget.pkg.github.com/$owner/index.json"

dotnet nuget list source
```
