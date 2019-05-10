```
// Table: Cross-Workspace Protected VMs with Protection State
// Replace workspaceName with a valid Workspace Name, between the quotation marks
let ProtectionDetail = datatable (ProtectionState_s: string, Verbose: string)
[
    "ProtectionStopped", "Backup is disabled. Please re-enable it in the Vault: ",
    "Protected", "Backup is configured in the Vault: ",
];
( AzureDiagnostics
    | where Category == "AzureBackupReport"
    | where ProtectionState_s != ""
    | summarize hint.strategy = partitioned arg_max(TimeGenerated, *) by BackupItemFriendlyName_s )
| join kind = rightouter (
    union Heartbeat, workspace("workspaceName").Heartbeat
    | summarize hint.strategy = partitioned arg_max(TimeGenerated, *) by Computer
    | project BackupItemFriendlyName_s = Computer )
    on BackupItemFriendlyName_s
| join kind = leftouter (
    ProtectionDetail )
    on ProtectionState_s
| extend BackupState = iif(isempty(ProtectionState_s),"Unprotected",ProtectionState_s)
| extend Description = iif(isempty(ProtectionState_s),"Backup is not configured.", Verbose)
| project SourcerName= BackupItemFriendlyName_s1 , BackupState , Explanation = strcat (Description, Resource)
| sort by SourceName asc
```
