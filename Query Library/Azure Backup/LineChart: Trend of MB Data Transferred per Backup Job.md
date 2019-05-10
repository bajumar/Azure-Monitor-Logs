```
// LineChart: Trend of MB Data Transferred per Backup Job
AzureDiagnostics
| where Category == "AzureBackupReport"
| where JobOperation_s == "Backup" and JobStatus_s == "Completed" and JobStartDateTime_s contains "Z"
| extend SourceName =  extract("([^;]+$)", 1, BackupItemUniqueId_s)
| extend DataMB = todouble(DataTransferredInMB_s) 
| project JobStartDateTime_s, SourceName, DataMB
| order by JobStartDateTime_s desc
| render timechart
```
