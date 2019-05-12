### LineChart: Trend of Resource Group Storage Consumption

```
// LineChart: Trend of Resource Group Storage Consumption
AzureDiagnostics
| where Category == "AzureBackupReport"
| where StorageConsumedInMBs_s != ""
| extend CloudStorageInGB = todouble(StorageConsumedInMBs_s) / 1024
| summarize sum(CloudStorageInGB) by bin(TimeGenerated, 1d), ResourceGroup
| render timechart
```
