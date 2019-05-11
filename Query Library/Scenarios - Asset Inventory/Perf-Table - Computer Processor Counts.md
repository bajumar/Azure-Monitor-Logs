```
// Perf-Table: Computer Processor Counts
// Requires enabling at least one Windows\Linux "Processor(*)\..." performance counter
// The required Windows counter IS NOT included in the default recommended set for Windows
// The required Linux counter IS included in the default recommended set for Linux
Perf
| where ObjectName == "Processor" and InstanceName != "_Total"
| summarize Processors = dcount(InstanceName) by Computer
| project Computer, Processors
| sort by Computer asc
```