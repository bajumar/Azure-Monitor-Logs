```
// PieChart: Completed vs Failed Backup Jobs
AzureDiagnostics
| where Category == "AzureBackupReport"
| where JobOperation_s == "Backup"
| extend SourceName =  extract("([^;]+$)", 1, BackupItemUniqueId_s)
| summarize AggregatedValue = dcount(JobUniqueId_g) by JobStatus_s, SourceName
| order by AggregatedValue desc
| render piechart
```
