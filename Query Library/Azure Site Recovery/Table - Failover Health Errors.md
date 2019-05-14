### Table: Failover Health Errors

```
// Table: Failover Health Errors
AzureDiagnostics
| where Category == "AzureSiteRecoveryReplicatedItems"
| where failoverHealth_s != "Normal"
| summarize hint.strategy=partitioned arg_max(TimeGenerated, *) by name_s
| mvexpand d = parsejson(failoverHealthErrors_s)
| extend errorCategory = tostring(d.errorCategory)
| extend errorCode = tostring(d.errorCode)
| extend errorLevel = tostring(d.errorLevel)
| extend errorMessage = tostring(d.errorMessage)
| extend creationTime = tostring(d.creationTime)
| extend possibleCauses = tostring(d.possibleCauses)
| extend recommendation = tostring(d.recommendation)
| project ComputerName = name_s, errorCategory, errorCode, errorLevel, errorMessage, creationTime, recommendation
| sort by errorLevel asc, ComputerName asc
```
