```
// LineChart: Trend of Backup Job Duration in Minutes
AzureDiagnostics
| where Category == "AzureBackupReport"
| where JobOperation_s == "Backup" and JobStatus_s == "Completed" and JobStartDateTime_s contains "Z" 
| extend SourceName =  extract("([^;]+$)", 1, BackupItemUniqueId_s)
| extend JobMinutes = todouble(JobDurationInSecs_s) / 60
| project JobStartDateTime_s, SourceName, JobMinutes
| order by JobStartDateTime_s desc 
| render timechart
```
