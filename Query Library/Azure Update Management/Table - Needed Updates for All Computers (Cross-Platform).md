### Table: Needed Updates for All Computers (Cross-Platform)

```
// Table: Needed Updates for All Computers (Cross-Platform)
Update
| where UpdateState == "Needed"
| summarize hint.strategy=partitioned arg_max(TimeGenerated, *) by Computer, SourceComputerId, UpdateID
| extend OSType = iff(isempty(OSType), "Windows", OSType)
| extend UpdateFor = iff(isempty(OSName), Product, OSName)
| extend Severity = iff(isempty(PackageSeverity), MSRCSeverity, PackageSeverity)
| extend ID = iff(isempty(BulletinID), iff(isnotempty(KBID),strcat("KB: ",KBID),""), strcat("Bulletin: ", BulletinID))
| extend Description = iff(isempty(CVENumbers), Title, CVENumbers)
| project Computer, OSType, UpdateFor , Classification, Severity, ID, Description, RebootBehavior
| sort by Computer asc
```
