```
// LineChart: Trend of Recovery Vault Storage Consumption
AzureDiagnostics
| where Category == "AzureBackupReport"
| where StorageConsumedInMBs_s != ""
| extend CloudStorageInGB = todouble(StorageConsumedInMBs_s) / 1024
| summarize sum(CloudStorageInGB) by bin(TimeGenerated, 1d), Vault = Resource
| render timechart
```
