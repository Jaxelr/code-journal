# Generating a self signed certificate on windows for IIS

1. Show the existing certificate: `netsh http show sslcert ipport=0.0.0.0:443`
1. Delete the existing one: netsh http `delete sslcert ipport=0.0.0.0:443`
1. Create the cert inside iis (Server Certificates)
1. Lastly run: `netsh http add sslcert ipport=0.0.0.0:443 certhash={hashgoeshere} appid={appidgoeshere}`

You can customly create certificates on powershell with the following command:

```powershell
New-SelfSignedCertificate -CertStoreLocation Cert:\LocalMachine\My -DnsName "mylocalsite.local" -FriendlyName "MyLocalSiteCert" -NotAfter (Get-Date).AddYears(10)
```

For more information check [ms docs](https://docs.microsoft.com/en-us/dotnet/framework/wcf/feature-details/how-to-configure-a-port-with-an-ssl-certificate)
