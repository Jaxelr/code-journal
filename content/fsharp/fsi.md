# F# Interactive

To invoke the fsi console, run `dotnet fsi` from any console, or on Vs Code run `FSI: Start` 

The following directives are available on fsi:

- Referencing nuget package on the fsi

```fsharp
#r "nuget: {{PackageName}}"
open {{namespace}}
```

- Referencing nuget package and version on the fsi

```fsharp
#r "nuget: {{PackageName}}, {{PackageVersion}}"
open {{namespace}}
```

- Referencing a package source

```fsharp
#i "nuget: {{PackageSourceUrl}}"
#i """nuget: {{NupkgPath}}"""
```

- Referencing assemblies on disk

```fsharp
#r "path/to/assembly.dll"
open {{namespace}}
```

- Loading other f# scripts

```fsharp
#load "path/to/Script1.fsx"
open Script1
```

- Quitting the fsi

```fsharp
#quit
```

- see help on the fsi

```fsharp
#help
```
