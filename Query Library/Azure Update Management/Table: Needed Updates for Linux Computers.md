```
// Table: Needed Updates for Linux Computers
Update
| where OSType == "Linux" and UpdateState == "Needed"
| summarize hint.strategy=partitioned arg_max(TimeGenerated, *) by Computer, SourceComputerId, UpdateID
| project Computer, OSName, Classification, PackageSeverity, BulletinID, CVENumbers
| sort by Computer asc
```
