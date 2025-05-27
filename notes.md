# Modify the following variables to match your environment
$managementManagementGroup = "The management group id for Management"

# Run the following commands to initiate remediation
.\patterns\alz\scripts\Start-AMBA-ALZ-Remediation.ps1 -managementGroupName $managementManagementGroup -policyName Alerting-Management

# Modify the following variables to match your environment
$location = "eastus"
$pseudoRootManagementGroup = "MG_Lids"
$platformManagementGroup = "MG_Lids_Platform"
$identityManagementGroup = "MG_Lids_Platform"
$managementManagementGroup = "MG_Lids_Platform"
$connectivityManagementGroup = "MG_Lids_Platform"
$LZManagementGroup = "MG_Lids_LandingZones"

# Run the following commands to initiate remediation
.\patterns\alz\scripts\Start-AMBA-ALZ-Remediation.ps1 -managementGroupName $pseudoRootManagementGroup -policyName Notification-Assets
.\patterns\alz\scripts\Start-AMBA-ALZ-Remediation.ps1 -managementGroupName $pseudoRootManagementGroup -policyName Alerting-ServiceHealth

## .\patterns\alz\scripts\Start-AMBA-ALZ-Remediation.ps1 -managementGroupName $platformManagementGroup -policyName Alerting-HybridVM

.\patterns\alz\scripts\Start-AMBA-ALZ-Remediation.ps1 -managementGroupName $platformManagementGroup -policyName Alerting-VM
.\patterns\alz\scripts\Start-AMBA-ALZ-Remediation.ps1 -managementGroupName $connectivityManagementGroup -policyName Alerting-Connectivity
.\patterns\alz\scripts\Start-AMBA-ALZ-Remediation.ps1 -managementGroupName $identityManagementGroup -policyName Alerting-Identity
.\patterns\alz\scripts\Start-AMBA-ALZ-Remediation.ps1 -managementGroupName $managementManagementGroup -policyName Alerting-Management

.\patterns\alz\scripts\Start-AMBA-ALZ-Remediation.ps1 -managementGroupName $LZManagementGroup -policyName Alerting-KeyManagement
.\patterns\alz\scripts\Start-AMBA-ALZ-Remediation.ps1 -managementGroupName $LZManagementGroup -policyName Alerting-LoadBalancing
.\patterns\alz\scripts\Start-AMBA-ALZ-Remediation.ps1 -managementGroupName $LZManagementGroup -policyName Alerting-NetworkChanges
.\patterns\alz\scripts\Start-AMBA-ALZ-Remediation.ps1 -managementGroupName $LZManagementGroup -policyName Alerting-RecoveryServices
.\patterns\alz\scripts\Start-AMBA-ALZ-Remediation.ps1 -managementGroupName $LZManagementGroup -policyName Alerting-Storage

## .\patterns\alz\scripts\Start-AMBA-ALZ-Remediation.ps1 -managementGroupName $LZManagementGroup -policyName Alerting-HybridVM
.\patterns\alz\scripts\Start-AMBA-ALZ-Remediation.ps1 -managementGroupName $LZManagementGroup -policyName Alerting-VM
## .\patterns\alz\scripts\Start-AMBA-ALZ-Remediation.ps1 -managementGroupName $LZManagementGroup -policyName Alerting-Web

New-AzManagementGroupDeployment -Name "amba-GeneralDeployment" -ManagementGroupId $pseudoRootManagementGroup -Location $location -TemplateUri "https://raw.githubusercontent.com/osterjeff/amba/refs/heads/main/patterns/alz/alzArm.json" -TemplateParameterFile ".\patterns\alz\alzArm.param.json"





.\Start-AzMigrateTest.ps1  -AZMigrateRG '3CloudAssessment'  -ProjectName 'vspheremigrationdiscovery'  -VMToMigrate 'HW-XCenterDB02'  -DestSubscription 'Shared-App-Prod'  -DestBubblevNet  'dev-lids-vnet-bubble'  -DestBubbleSubnet 'Open' -ProdSubscription 'Infrastructure and Technical Operations' -TenantId '0c899ad0-da83-4b2e-a353-672e31595333'  -ValidateOnly 