```
// LineChart: Trend of Source Storage Consumption
AzureDiagnostics
| where Category == "AzureBackupReport"
| where StorageConsumedInMBs_s != "" 
| extend SourceName =  extract("([^;]+$)", 1, BackupItemUniqueId_s)
| extend CloudStorageInGB = todouble(StorageConsumedInMBs_s) / 1024
| summarize sum(CloudStorageInGB) by bin(TimeGenerated, 1d), SourceName
| render timechart
```
