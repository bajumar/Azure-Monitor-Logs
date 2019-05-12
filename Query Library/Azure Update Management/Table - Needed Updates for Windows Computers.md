### Table: Needed Updates for Windows Computers

```
// Table: Needed Updates for Windows Computers
Update
| where OSType != "Linux" and UpdateState == "Needed"
| summarize hint.strategy=partitioned arg_max(TimeGenerated, *) by Computer, SourceComputerId, UpdateID
| project Computer, Product, Classification, MSRCSeverity, KBID, Title, RebootBehavior
| sort by Computer asc
```
