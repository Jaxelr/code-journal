# Azure cli commands

Index of commands related to the azure cli.

## Account

### Subscription

- Set appropiate subscription: `az account set --subscription "{subscription}"`

## CosmosDB

### Container

- Create container: `az cosmosdb sql container create --account-name "{account}" --database-name "{database}" --name "{container}" --partition-key-path "/{partitionKey} --resource-group "{resourceGroup}"`
- Grant read-write role `az cosmosdb sql role assignment create --account-name "{account}" --resource-group "{resourceGroup}"  --scope "/" --principal-id {principal} --role-definition-id {role-id}`
- To find the role definition that exists on the cosmos: `az cosmosdb sql role definition list --account-name "{account}" --resource-group "{resourceGroup}"`

## Frontdoor

### Route 

- Update route: `az afd route update -g {resourceGroup} --profile-name {profile} --endpoint-name {endpoint} --name {route-name} --origin-group {origin-group} `

## AKV

### Certificate

- Show certificate: `az keyvault certificate show --vault-name "{vault}" --name "{certificate}"`
- Get certificate: `az keyvault certificate download --vault-name "{vault}" --name "{certificate}" --file "{file}.cer"`

### Secrets

- List secrets: `az keyvault secret list --vault-name "{vault}"`
- Show secrets: `az keyvault secret show --vault-name "{vault}" --name "{secret}"`
- Get Secret value: `az keyvault secret show --vault-name "{vault}" --name "{secret}" --query value -o tsv`