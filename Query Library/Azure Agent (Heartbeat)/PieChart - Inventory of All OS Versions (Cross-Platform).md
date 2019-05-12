### PieChart: Inventory of All OS Versions (Cross-Platform)

```
// PieChart: Inventory of All OS Versions (Cross-Platform)
let VersionMap = datatable (Version: string, ReleaseName:string)
[
    "10.0", "Server 2016/2019",
     "6.3", "Server 2012 R2",
     "6.2", "Server 2012",
     "6.1", "Server 2008 R2",
     "6.0", "Server 2008",
     "5.2", "Server 2003/2003 R2",
     "5.0", "Server 2000"
];
Heartbeat
| summarize hint.strategy=partitioned arg_max(TimeGenerated, *) by Computer
| extend Version = strcat(OSMajorVersion, ".", OSMinorVersion)
| join kind = leftouter(VersionMap) on Version
| extend OSName = iif(isempty(OSName), strcat(OSType, " ", ReleaseName), OSName)
| summarize count() by ComputerEnvironment, OSType, OSName
| render piechart
```
