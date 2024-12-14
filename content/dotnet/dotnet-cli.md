# Dotnet Cli 

Some obscure dotnet cli commands I have encountered:

- List all installed Sdks

Run `dotnet --list-sdks`

- List all installed runtimes

Run `dotnet --list-runtimes`

Newer cli versions support `dotnet sdk check`

- List installation information

Run `dotnet --info`

- Restarting dotnet new -l packages

Run `dotnet new --debug:reinit`

Format the code to match the editorconfig settings

`dotnet format <Sln/Csproj>`

Another favorite is `dotnet format whitespace` which will match the settings for whitespace.