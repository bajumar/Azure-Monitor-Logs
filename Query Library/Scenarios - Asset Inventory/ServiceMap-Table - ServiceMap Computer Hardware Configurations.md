```
// ServiceMap-Table: ServiceMap Computer Hardware Configurations
// You can also generate useful charts from the data returned by this query
ServiceMapComputer_CL
| summarize hint.strategy=partitioned arg_max(TimeGenerated, *) by Computer
| extend ["Operating System"]= extract("([^,]+$)", 1, OperatingSystemFullName_s)
| extend AKSRegion = extract("([^_]+$)", 1, AzureResourceGroup_s)
| extend ["Memory (GB)"] = round(PhysicalMemory_d/1024)
| extend ["Azure VM Size"] = iff(isempty(HostingProvider_s), "N/A - not an Azure VM", iff(Computer startswith "aks", "N/A - AKS Container", AzureVMSize_s))
| extend ["Azure Region"] = iff(isempty(HostingProvider_s), "N/A - not an Azure VM", iff(Computer startswith "aks", AKSRegion, AzureLocation_s))
| project Computer, ["Operating System"], Processors = Cpus_d, ["Memory (GB)"], ["Memory (KB)"] = PhysicalMemory_d, ["IPv4 Address(es)"] = Ipv4Addresses_s, ["Azure VM Size"], ["Azure Region"]
| sort by Computer
```