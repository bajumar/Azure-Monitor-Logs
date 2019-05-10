```
// Table: All Backup Alerts
AzureDiagnostics
| where Category == "AzureBackupReport"
| where AlertCode_s != ""
| extend SourceName =  extract("([^;]+$)", 1, BackupItemUniqueId_s)
| project SourceName, AlertCode_s, AlertSeverity_s, AlertStatus_s , AlertOccurrenceDateTime_s
| sort by SourceName asc
```
