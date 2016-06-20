# Azure DE automation

## 1. Powershell
Requires Azure Powershell

### 1.1 List available environments
Currently the powershell profile does not contain the AzureDE enviroment.
If `Get-AzureRmEnvironment | Select Name` contains `AzureGermany` these steps are not required anymore: skip to 1.3.

### 1.2 <your-de-login>

1. Download `https://raw.githubusercontent.com/gitralf/powershell/master/examples/mcdprofile.json`
2. Rename to azuregermany.json
3. Import: `Select-AzureRmProfile -Path c:\ps\azuregermany.json` (absolute path required)
4. Register: `Add-AzureRmAccount -EnvironmentName AzureGermany` (and complete the log-in flow)

## 2. azure-cli
`azure login -u <your-de-login>`
