# Azure Cloud Shell Commands

Index of commands related to the azure cloud shell.

## Commands


## Key Vaults

### Keyvault

- Get key vault info: `Get-AzKeyVault -VaultName "{name}"`
- Remove key vault info: `Remove-AzKeyVault -VaultName "{name}"`
- Get key vault info soft deleted: `Get-AzKeyVault -VaultName "{name}" -InRemovedState`
- Recover soft deleted KV: `Undo-AzKeyVaultRemoval -VaultName "{name}"`
- Purge KV: `Remove-AzKeyVault -VaultName "{name}" -InRemovedState`

### Certificates

- Access Policy to certificates: `Set-AzKeyVaultAccessPolicy -VaultName "{name}" -UserPrincipalName {principal} -PermissionsToCertificates recover,purge`
- Get certificate: `Get-AzKeyVaultCertificate -VaultName "{name}"`
- Get certificate in soft delete state: `Get-AzKeyVaultCertificate -VaultName "{name}" -InRemovedState`
- Restore certificate in deleted state: `Undo-AzKeyVaultCertificateRemoval -VaultName "{name}" -Name "{certname}"`
- Remove certificate: `Remove-AzKeyVaultCertificate -VaultName "{name}" -Name "{certname}"`
- Remove certificate in soft delete state: `Remove-AzKeyVaultCertificate -VaultName "{name}" -Name "{certname}" -InRemovedState`
- Export certificate from vault:  

```powershell
$cert = Get-AzKeyVaultCertificate -VaultName "{name}" -Name "{certname}"
$secret = Get-AzKeyVaultSecret -VaultName "{name}" -Name $cert.Name
$secretValueText = '';
$ssPtr = [System.Runtime.InteropServices.Marshal]::SecureStringToBSTR($secret.SecretValue)
try {
    $secretValueText = [System.Runtime.InteropServices.Marshal]::PtrToStringBSTR($ssPtr)
} finally {
    [System.Runtime.InteropServices.Marshal]::ZeroFreeBSTR($ssPtr)
}
$secretByte = [Convert]::FromBase64String($secretValueText)
$x509Cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($secretByte,'','Exportable,PersistKeySet')
$type = [System.Security.Cryptography.X509Certificates.X509ContentType]::Pfx
$pfxFileByte = $x509Cert.Export($type, $password)

# Write to file
[System.IO.File]::WriteAllBytes("{certname}.pfx", $pfxFileByte)
```

### Keys

- Access Policy to keys: `Set-AzKeyVaultAccessPolicy -VaultName "{name}" -UserPrincipalName {principal} -PermissionsToKeys recover,purge`
- Get key: `Get-AzKeyVaultKey -VaultName "{name}"`
- Get key in soft delete state: `Get-AzKeyVaultKey -VaultName "{name}" -InRemovedState`
- Restore key in deleted state: `Undo-AzKeyVaultKeyRemoval -VaultName "{name}" -Name "{keyname]"`
- Remove key: `Remove-AzKeyVaultKey -VaultName "{name}" -Name "{keyname]"`
- Remove key in soft delete state: `Remove-AzKeyVaultKey -VaultName "{name}" -Name "{keyname]" -InRemovedState`

### Secrets

- Access Policy to secrets: `Set-AzKeyVaultAccessPolicy -VaultName "{name}" -UserPrincipalName {principal} -PermissionsToSecrets recover,purge`
- Get secret: `Get-AzKeyVaultSecret -VaultName "{name}"`
- Get secret as text: `Get-AzKeyVaultSecret -VaultName "{name}" -AsPlainText`
- Get secret in soft delete state: `Get-AzKeyVaultSecret -VaultName "{name}" -InRemovedState`
- Restore secret in deleted state: `Undo-AzKeyVaultSecretRemoval -VaultName "{name}" -Name "{secretname]"`
- Remove secret: `Remove-AzKeyVaultSecret -VaultName "{name}" -Name "{secretname]"`
- Remove secret in soft delete state: `Remove-AzKeyVaultSecret -VaultName "{name}" -Name "{secretname]" -InRemovedState`

#### Troubleshooting

- If you get an error like `Operation returned an invalid status code 'Forbidden'. Public network access is disabled`, you need to enable networking access for the Azure Cloud Shell. First, you will need to find out your ip from cloud shell by running `curl -s checkip.dyndns.org | sed -e 's/.*Current IP Address: //' -e 's/<.*$//'
` next you will need to allow list that ip.
- If you get an error like `Client address is not authorized and caller is not a trusted service'`, make sure your ip is allowlisted.
