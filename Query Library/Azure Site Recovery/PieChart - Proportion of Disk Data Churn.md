### PieChart: Proportion of Disk Data Churn

```
// PieChart: Proportion of Disk Data Churn
AzureDiagnostics
| where Category == "AzureSiteRecoveryProtectedDiskDataChurn"
| extend ComputerName = extract("(.*?):",1, InstanceName_s)
| extend VaultName = Resource
| extend VaultResourceGroup = ResourceGroup
| summarize DataChurnKB = max(toint(Value_s)/1024) by TimeGenerated, ComputerName, VaultName, VaultResourceGroup
| render piechart
```
