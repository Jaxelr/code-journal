# Shells

Index of snippets and commands that are useful for day to day troubleshooting:

## Powershell

- Restart remote computer - [Restart-Computer](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.management/restart-computer?view=powershell-7.1)
- Count files in a path (recursively) `(Get-ChildItem -File -Recurse -Filter *.rdl | Measure-Object).Count`
- Set environment variable `setx ASPNETCORE_ENVIRONMENT "Development"`
- More complex snippets that i use daily can be found on this [shellscripts repository](https://github.com/Jaxelr/ShellScripts)
