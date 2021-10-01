# Add readme.md on project (csproj) 

This works for the new UI version of dotnet. More information [here](https://docs.microsoft.com/en-us/nuget/nuget-org/package-readme-on-nuget-org)

- Include on property group the tag of packagereadmefile:

```xml
  <PropertyGroup>
    <PackageReadmeFile>readme.md</PackageReadmeFile>
  </PropertyGroup>
```

- Add an item group with the readme.md file

```xml
  <ItemGroup>
    <None Include="readme.md">
      <Pack>True</Pack>
      <PackagePath>\</PackagePath>
    </None>
  </ItemGroup>
```

> Package path is the output location of the file
