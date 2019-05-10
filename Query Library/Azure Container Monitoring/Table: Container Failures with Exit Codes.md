```
// Table: Container Failures with Exit Codes
ContainerInventory
| where ContainerState == "Failed"
| summarize Failures = dcount(ContainerID) by Computer, Image, ExitCode
| sort by Failures
```
