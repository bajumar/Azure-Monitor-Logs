### LineChart: Trend of Disk Data Churn

```
// LineChart: Trend of Disk Data Churn
AzureDiagnostics
| where Category == "AzureSiteRecoveryProtectedDiskDataChurn"
| extend ComputerName = extract("(.*?):",1, InstanceName_s)
| extend VaultName = Resource
| extend VaultResourceGroup = ResourceGroup
| summarize DataChurnKB = avg(toint(Value_s)/1024) by TimeGenerated, ComputerName, VaultName, VaultResourceGroup
| render timechart
```
