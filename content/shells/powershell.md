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
- If needed be, you can split the values as based on the delimiters from the field, considering the case of the Path var, you can run `$env:Path  -split ';'` to obtain a list of the values.

![image](https://user-images.githubusercontent.com/5913008/163220227-505b7c29-e129-4d41-9343-05702664f10f.png)

