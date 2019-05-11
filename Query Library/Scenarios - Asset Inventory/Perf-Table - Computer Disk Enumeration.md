```
// Perf-Table: Computer Disk Enumeration
// Requires enabling at least one Windows "LogicalDisk(*)\..." and Linux "Physical Disk(*)\..." performance counter
// The required Windows counter IS included in the default recommended set for Windows
// The required Linux counter IS NOT included in the default recommended set for Linux
Perf
| where ObjectName == "LogicalDisk" or ObjectName == "Physical Disk"
| where InstanceName != "_Total" and InstanceName !startswith "Harddisk"
| summarize makeset(InstanceName) by Computer
| project Computer, ["Assigned Disks"] = set_InstanceName
| sort by Computer asc
```