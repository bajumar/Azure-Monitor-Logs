### Table: Computer Hardware Configurations

```
// Table: Computer Hardware Configurations
ServiceMapComputer_CL
| summarize hint.strategy=partitioned arg_max(TimeGenerated, *) by Computer
| extend ["Operating System"]= extract("([^,]+$)", 1, OperatingSystemFullName_s)
| extend dNICs = parsejson(Ipv4Addresses_s) 
| extend NICs = arraylength(dNICs)
| extend ["Ephemeral Disk"] = iff(isempty(HostingProvider_s), "N/A - not an Azure VM", iff(OperatingSystemFullName_s startswith "L", "Disk 'sdb' is ephemeral.", "Disk 'D' is ephemeral."))
| project Computer, ["Operating System"], Processors = Cpus_d, ["Memory (KB)"] = PhysicalMemory_d, ["Ephemeral Disk"], NICs, ["IPv4 Address(es)"] = Ipv4Addresses_s
| sort by Computer
| join kind = leftouter (
   Perf
   | where ObjectName == "LogicalDisk" or ObjectName == "Physical Disk"
   | where InstanceName != "_Total" and InstanceName !startswith "Harddisk"
   | summarize dDisks = makeset(InstanceName) by Computer
   | extend Disks = arraylength(dDisks)
   | project Computer, Disks, ["Assigned Disks"] = dDisks
) on Computer
| project Computer, ["Operating System"], Processors, ["Memory (KB)"], Disks, ["Assigned Disks"], ["Ephemeral Disk"], NICs, ["IPv4 Address(es)"]
| sort by Computer asc
```