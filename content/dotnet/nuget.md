# Nuget 

## Sources

- To add a source: `dotnet nuget add source <url> -n <name>`
- To enable a source run: `dotnet nuget enable source <name>`
- To disable a source run: `dotnet nuget disable source <name>`
- To remove a source: `dotnet nuget remove source <name>`

## Caches

From the command line run the following commands: `dotnet nuget locals all --clear`

Or using the nuget cli: `nuget locals all -clear`

The cache location should be here `%userprofile%\.nuget\packages`
