```
// ServiceMap-PieChart: ServiceMap Computer Azure Region Locations
// Before saving or pinning, enable the "Split By" values of your preference to make the visulaization more impactful
ServiceMapComputer_CL
| summarize hint.strategy=partitioned arg_max(TimeGenerated, *) by Computer
| extend ["Operating System"]= extract("([^,]+$)", 1, OperatingSystemFullName_s)
| extend AKSRegion = extract("([^_]+$)", 1, AzureResourceGroup_s)
| extend ["Memory (GB)"] = round(PhysicalMemory_d/1024)
| extend ["Azure VM Size"] = iff(isempty(HostingProvider_s), "N/A - not an Azure VM", iff(Computer startswith "aks", "N/A - AKS Container", AzureVMSize_s))
| extend ["Azure Region"] = iff(isempty(HostingProvider_s), "N/A - not an Azure VM", iff(Computer startswith "aks", AKSRegion, AzureLocation_s))
| project Computer, ["Operating System"], ["Azure VM Size"], ["Azure Region"]
| summarize count() by ["Azure Region"], ["Azure VM Size"], ["Operating System"], Computer
| render piechart
```