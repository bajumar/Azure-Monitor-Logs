```
// Perf-Table: Computer Disk Enumeration
// Requires one Linux "Physical Disk(*)\..." and one Windows "LogicalDisk(*)\..."
Perf
| where ObjectName == "Physical Disk" or ObjectName == "LogicalDisk"
| where InstanceName != "_Total" and InstanceName !startswith "Harddisk"
| summarize makeset(InstanceName) by Computer
| project Computer, ["Enumerated Disks"] = set_InstanceName
| sort by Computer asc
```