# Shells

Index of snippets and commands that are useful for day to day troubleshooting:

## Powershell

- Restart remote computer - [Restart-Computer](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.management/restart-computer?view=powershell-7.1)
- Count files in a path (recursively) `(Get-ChildItem -File -Recurse -Filter *.rdl | Measure-Object).Count`
- More complex snippets that i use daily can be found on this [shellscripts repository](https://github.com/Jaxelr/ShellScripts)

### Environment variables

- Set environment variable `setx ASPNETCORE_ENVIRONMENT "Development"` for current session
- Set environment variable permanently `[System.Environment]::SetEnvironmentVariable('ASPNETCORE_ENVIRONMENT','Development')`
- Get environment variables using `Get-ChildItem -Path Env:` or if needed individually `Get-ChildItem -Path Env:ASPNETCORE_ENVIRONMENT`
