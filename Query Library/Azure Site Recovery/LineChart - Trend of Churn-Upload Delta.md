### LineChart: Trend of Churn-Upload Delta

```
// LineChart: Trend of Churn-Upload Delta
AzureDiagnostics
| where Category == "AzureSiteRecoveryProtectedDiskDataChurn"
| summarize DataChurnKB = avg(toint(Value_s)/1024) by TimeGenerated, InstanceName_s, Resource, ResourceGroup
| join kind = leftouter (
  AzureDiagnostics
  | where Category == "AzureSiteRecoveryReplicationDataUploadRate"
  | summarize DataUploadKB = avg(toint(Value_s)/1024) by TimeGenerated, InstanceName_s, Resource, ResourceGroup
) on TimeGenerated
| extend ComputerName = extract("(.*?):",1, InstanceName_s)
| extend VaultName = Resource
| extend VaultResourceGroup = ResourceGroup
| summarize ["Churn Minus Upload Delta (KB)"] = sum(DataChurnKB-DataUploadKB) by TimeGenerated, ComputerName, VaultName, VaultResourceGroup
| render timechart
```
