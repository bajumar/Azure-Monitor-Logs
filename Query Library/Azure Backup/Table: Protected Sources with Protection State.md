```
// Table: Protected Sources with Protection State
AzureDiagnostics
| where Category == "AzureBackupReport"
| where ProtectionState_s !=  ""
| summarize hint.strategy = partitioned arg_max(TimeGenerated, *) by BackupItemFriendlyName_s
| project SourceName = BackupItemFriendlyName_s, ProtectionState_s, Vault = Resource, TimeGenerated
| sort by SourceName asc
```
