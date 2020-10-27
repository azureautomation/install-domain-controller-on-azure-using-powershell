Install Domain Controller on Azure using Powershell
===================================================

            
This Script was created to Install Domain Controller
**on Azure VM.**


Simply edit the PS1 file based on the comments in the file to match your environment and you will have a simple way of deploying Domain controller.


Be sure to take note of the comments in the PS1 file to insert your input according to your environment.



PowerShell
Edit|Remove
powershell
## Enter your domain name e.g. lab.local
## Enter netBios Name e.g. lab
## Enter safe password e.g. Passw0rd

$regkey = test-path hklm:\software\FTCAD
if ($regkey -eq $true) {exit}
else {
# Turn Off Windows Firewall
netsh advfirewall set allprofiles state off
# Set Winrm trust for remote powershell
Set-Item wsman:\localhost\client\trustedhosts * -Force
# Install ADDS prerequisites
Add-WindowsFeature RSAT-AD-Tools
Add-WindowsFeature -Name 'ad-domain-services' -IncludeAllSubFeature -IncludeManagementTools
Add-WindowsFeature -Name 'dns' -IncludeAllSubFeature -IncludeManagementTools 
Add-WindowsFeature -Name 'gpmc' -IncludeAllSubFeature -IncludeManagementTools
REG ADD HKLM\Software\FTCAD /v Data /t Reg_SZ /d 'Installed'
# Windows PowerShell script for AD DS Deployment
$domainname = 'lab.local' 
$netbiosName = 'lab' 
$safemodepassword = 'Passw0rd' | ConvertTo-SecureString -AsPlainText -Force
Import-Module ADDSDeployment
Install-ADDSForest `
-CreateDnsDelegation:$false `
-DatabasePath 'C:\Windows\NTDS' `
-DomainMode 'Win2012' `
-DomainName $domainname `
-DomainNetbiosName $netbiosName `
-ForestMode 'Win2012' `
-InstallDns:$True `
-LogPath 'C:\Windows\NTDS' `
-NoRebootOnCompletion:$false `
-SafeModeAdministratorPassword $safemodepassword `
-SysvolPath 'C:\Windows\SYSVOL' `
-Force:$true}
# POWERSHELL TO EXECUTE ON REMOTE SERVER ENDS HERE



## Enter your domain name e.g. lab.local 
## Enter netBios Name e.g. lab 
## Enter safe password e.g. Passw0rd 
 
$regkey = test-path hklm:\software\FTCAD 
if ($regkey -eq $true) {exit} 
else { 
# Turn Off Windows Firewall 
netsh advfirewall set allprofiles state off 
# Set Winrm trust for remote powershell 
Set-Item wsman:\localhost\client\trustedhosts * -Force 
# Install ADDS prerequisites 
Add-WindowsFeature RSAT-AD-Tools 
Add-WindowsFeature -Name 'ad-domain-services' -IncludeAllSubFeature -IncludeManagementTools 
Add-WindowsFeature -Name 'dns' -IncludeAllSubFeature -IncludeManagementTools  
Add-WindowsFeature -Name 'gpmc' -IncludeAllSubFeature -IncludeManagementTools 
REG ADD HKLM\Software\FTCAD /v Data /t Reg_SZ /d 'Installed' 
# Windows PowerShell script for AD DS Deployment 
$domainname = 'lab.local'  
$netbiosName = 'lab'  
$safemodepassword = 'Passw0rd' | ConvertTo-SecureString -AsPlainText -Force 
Import-Module ADDSDeployment 
Install-ADDSForest ` 
-CreateDnsDelegation:$false ` 
-DatabasePath 'C:\Windows\NTDS' ` 
-DomainMode 'Win2012' ` 
-DomainName $domainname ` 
-DomainNetbiosName $netbiosName ` 
-ForestMode 'Win2012' ` 
-InstallDns:$True ` 
-LogPath 'C:\Windows\NTDS' ` 
-NoRebootOnCompletion:$false ` 
-SafeModeAdministratorPassword $safemodepassword ` 
-SysvolPath 'C:\Windows\SYSVOL' ` 
-Force:$true} 
# POWERSHELL TO EXECUTE ON REMOTE SERVER ENDS HERE 
 





You can use this script in following steps:    



  *  Download the script and copy it to your Server.

  *  Open it using PowerShell 
  *  Scroll down to the middle of the script file, and then add your domain name,  netbois name and
Credentials to install DC. 
  *  Save the file and then run the script on the computer.


    
TechNet gallery is retiring! This script was migrated from TechNet script center to GitHub by Microsoft Azure Automation product group. All the Script Center fields like Rating, RatingCount and DownloadCount have been carried over to Github as-is for the migrated scripts only. Note : The Script Center fields will not be applicable for the new repositories created in Github & hence those fields will not show up for new Github repositories.
