### Table: Computer CPU Counts

```
// Table: Computer CPU Counts
// Requires one Linux "Processor(*)\..." and one Windows "Processor(*)\..." 
Perf
| where ObjectName == "Processor" and InstanceName != "_Total"
| summarize Processors = dcount(InstanceName) by Computer
| project Computer, Processors
| sort by Computer asc
```