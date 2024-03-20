# Azure cli commands

Index of commands related to the azure cli.

## Account

### Subscription

- Set appropiate subscription: `az account set --subscription "{subscription}"`

## CosmosDB

### Container

- Create container: `az cosmosdb sql container create --account-name "{account}" --database-name "{database}" --name "{container}" --partition-key-path "/{partitionKey} --resource-group "{resourceGroup}"`

## Frontdoor

### Route 

- Update route: `az afd route update -g {resourceGroup} --profile-name {profile} --endpoint-name {endpoint} --name {route-name} --origin-group {origin-group}`