### Table: Inventory of Windows OS Versions

```
// Table: Inventory of Windows OS Versions
let VersionMap = datatable (Version: string, ReleaseName:string)
[
    "10.0", "Server 2016/2019",
     "6.3", "Server 2012 R2",
     "6.2", "Server 2012",
     "6.1", "Server 2008 R2",
     "6.0", "Server 2008",
     "5.2", "Server 2003/R2",
     "5.0", "Server 2000"
];
Heartbeat
| where OSType == "Windows"
| summarize hint.strategy=partitioned arg_max(TimeGenerated, *) by Computer
| extend Version = strcat (OSMajorVersion, ".", OSMinorVersion)
| join kind = leftouter(VersionMap) on Version
| extend OSName = strcat(OSType, " ", ReleaseName)
| project Computer, OSType, OSName, Version, ComputerIP, ComputerEnvironment
| sort by Computer asc
```
