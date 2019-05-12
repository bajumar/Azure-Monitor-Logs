### Table: Restore Jobs Status for All Sources

```
// Table: Restore Jobs Status for All Sources
AzureDiagnostics
| where Category == "AzureBackupReport"
| where JobOperation_s == "Restore" and JobStartDateTime_s contains "Z" 
| extend SourceName =  extract("([^;]+$)", 1, BackupItemUniqueId_s)
| extend JobMinutes = todouble(JobDurationInSecs_s) / 60
| project SourceName, JobStatus_s, JobFailureCode_s, JobStartDateTime_s, JobMinutes, Vault = Resource
| sort by SourceName asc
```
