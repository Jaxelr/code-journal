# Reading embedded resources from Assembly

The file must be declared in build action as Embedded resource

![Embedded Resource](images/embedded.png)

```csharp
    var assembly = Assembly.GetExecutingAssembly();
    
    string resource = ConfigurationManager.AppSettings["EmailResource"];
    
    using (Stream stream = assembly.GetManifestResourceStream(resource))
    using (StreamReader reader = new StreamReader(stream))
    {
        return reader.ReadToEnd();
    }
```
