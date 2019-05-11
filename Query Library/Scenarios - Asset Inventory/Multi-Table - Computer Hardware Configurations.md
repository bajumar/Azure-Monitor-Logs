```
// Multi-Table: Computer Hardware Configurations
// Requires enabling at least one Windows "LogicalDisk(*)\..." and Linux "Physical Disk(*)\..." performance counter
// The required Windows counter IS included in the default recommended set for Windows
// The required Linux counter IS NOT included in the default recommended set for Linux
ServiceMapComputer_CL
| summarize hint.strategy=partitioned arg_max(TimeGenerated, *) by Computer
| extend ["Operating System"]= extract("([^,]+$)", 1, OperatingSystemFullName_s)
| extend ["Ephemeral Disk"] = iff(isempty(HostingProvider_s), "N/A - not an Azure VM", iff(OperatingSystemFullName_s startswith "L", "Disk 'sdb' is ephemeral.", "Disk 'D' is ephemeral."))
| project Computer, ["Operating System"], Processors = Cpus_d, ["Memory (KB)"] = PhysicalMemory_d, ["Ephemeral Disk"], ["IPv4 Address(es)"] = Ipv4Addresses_s
| sort by Computer
| join kind= leftouter (
   Perf
   | where ObjectName == "LogicalDisk" or ObjectName == "Physical Disk"
   | where InstanceName != "_Total" and InstanceName !startswith "Harddisk"
   | summarize makeset(InstanceName) by Computer
   | project Computer, ["Assigned Disk(s)"] = set_InstanceName
) on Computer
| project Computer, ["Operating System"], Processors, ["Memory (KB)"], ["Assigned Disk(s)"], ["Ephemeral Disk"], ["IPv4 Address(es)"]
| sort by Computer asc
```