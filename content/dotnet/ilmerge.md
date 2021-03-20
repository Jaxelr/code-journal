# Implementing Ilmerge to merge DLLs into single file

This works solely on the .Net 4.X frameworks:

1. via Nuget `Install-Package ilmerge`
1. via Nuget `Install-Package ilmerge.msbuild.task`

You can *optionally() configure properties by using a ilmergeConfig.json file

```json
{
    "General": {
        "OutputFile": null,
        "TargetPlatform": null,
        "KeyFile": null,
        "AlternativeILMergePath": null,
        "InputAssemblies": []
    },
    "Advanced": {
        "AllowDuplicateType": null,
        "AllowMultipleAssemblyLevelAttributes": false,
        "AllowWildCards": false,
        "AllowZeroPeKind": false,
        "AttributeFile": null,
        "Closed": false,
        "CopyAttributes": false,
        "DebugInfo": true,
        "DelaySign": false,
        "ExcludeFile": "",
        "FileAlignment": 512,
        "Internalize": false,
        "Log": false,
        "LogFile": null,
        "PublicKeyTokens": true,
        "SearchDirectories": [],
        "TargetKind": null,
        "UnionMerge": true,
        "Version": null,
        "XmlDocumentation": false
    }
}
```

Alternatively, add the following bat file to use with ilmerge after build:

```bat
REM Manually build the file, jic ILMerge.MSBuild fails.
REM There's no need to use this file unless you are stuck with the build.
REM Always always always, test the dependencies on the target server, since they become picky in a hurry.

mkdir build-output
REM ITs important that you check the installed version
cp "../packages/ILmerge.2.14.1208/tools/ilmerge.exe" "build-output/ilmerge.exe"
xcopy "../src/bin/Release" build-output /E
cd build-output
rm -rf *.pdb
rm -rf *.xml
ilmerge.exe /log:../log.txt /allowDup /wildcards /out:Executable.exe Executable.exe *.dll
mv Executable.exe.config ../Executable.exe.config
mv Executable.exe ../Executable.exe
cd ..
rm -rf build-output/
Exit

```

Also, on windows 10 you can use [Costura.Fody](https://github.com/Fody/Costura)
