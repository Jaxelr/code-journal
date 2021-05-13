# Encrypt / Decrypt web config

How to encrypt/decrypt from iis the connection strings on the web.config file.

How to encrypt the connection strings on web.config (replace {app} with the location of the app on iis): 

`C:\Windows\Microsoft.NET\Framework\v4.0.30319\aspnet_regiis.exe -pe "connectionStrings" -app "/{app}"`

Grant permission to RSA key on the site:

`C:\Windows\Microsoft.NET\Framework\v4.0.30319\aspnet_regiis.exe -pa "NetFrameworkConfigurationKey" "NT AUTHORITY\NETWORK SERVICE"`

How to decrypt the connection strings on web.config (replace {app} with the location of the app on iis):

`C:\Windows\Microsoft.NET\Framework\v4.0.30319\aspnet_regiis.exe -pd "connectionStrings" -app "/{app}"`