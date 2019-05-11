```
// Table: Inventory of Linux OS Versions
Heartbeat
| where OSType == "Linux"
| summarize hint.strategy=partitioned arg_max(TimeGenerated, *) by Computer
| extend Version = strcat(OSMajorVersion, ".", OSMinorVersion)
| project Computer, OSType, OSName, Version, ComputerIP, ComputerEnvironment
| sort by Computer asc
```
