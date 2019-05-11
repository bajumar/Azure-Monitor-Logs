```
// Perf-Table: Computer Disk Counts
// Requires one Linux "Physical Disk(*)\..." and one Windows "LogicalDisk(*)\..."
Perf
| where ObjectName == "Physical Disk" or ObjectName == "LogicalDisk"
| where InstanceName != "_Total" and InstanceName !startswith "Harddisk"
| summarize Disks = dcount(InstanceName) by Computer
| project Computer, Disks
| sort by Computer asc
```