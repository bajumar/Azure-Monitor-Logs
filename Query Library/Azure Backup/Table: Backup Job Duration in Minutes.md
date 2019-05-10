```
// Table: Backup Job Duration in Minutes
AzureDiagnostics
| where Category == "AzureBackupReport"
| where JobOperation_s == "Backup" and JobStatus_s == "Completed" and JobStartDateTime_s contains "Z" 
| extend SourceName =  extract("([^;]+$)", 1, BackupItemUniqueId_s)
| extend JobMinutes = todouble(JobDurationInSecs_s) / 60
| project SourceName, JobMinutes
| order by JobMinutes desc
```
