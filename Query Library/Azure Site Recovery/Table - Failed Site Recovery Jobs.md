### Table: Failed Site Recovery Jobs

```
// Table: Failed Site Recovery Jobs
AzureDiagnostics
| where Category == "AzureSiteRecoveryJobs"
| where ResultType == "Failed"
| extend ComputerName = affectedResourceName_s
| extend ComputerType = affectedResourceType_s
| extend VaultName = Resource
| extend VaultResourceGroup = ResourceGroup
| summarize FailureCount = count(ResultType) by ComputerName, ComputerType, SourceSystem, OperationName, VaultName, VaultResourceGroup
| sort by ComputerName asc, OperationName asc
```
