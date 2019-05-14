## PieChart: Proportion of Average Disk Data Churn

```
// PieChart: Proportion of Average Disk Data Churn
AzureDiagnostics
| where Category == "AzureSiteRecoveryProtectedDiskDataChurn"
| extend ComputerName = extract("(.*?):",1, InstanceName_s)
| extend VaultName = Resource
| extend VaultResourceGroup = ResourceGroup
| summarize DataChurnKB = avg(toint(Value_s)/1024) by TimeGenerated, ComputerName, VaultName, VaultResourceGroup
| render piechart
```

### What are the key metrics?

**Protected Disk Data Churn** is the rate of change in data volume written to a computer's local disk (how much data is written in a given time period), measured in Bytes. This is converted to KB in the query.

The data is plotted in a pie chart, indication the proportion of total Churn data volume each computer contributes.

### Why is this useful?

Computers which generate a significant amount of Churn impact the efficiency of replication. The replication process may need to consume more bandwidth and/or take longer to process the changed data before a computer reaches "steady-state" to execute a successful planned failover.

If there appears to be a computer producing a disproportionate amount of Churn data volume relative to its workload peers, the behaviour be caused by one or more of the following issues:

| Possible Issue | What to Investigate |
| --- | --- | 
| The application or connected client activity is overwhelming the local disk. | Verify that local disk activity is within expected operational parameters. |
| The behaviour is expected for the assigned workload. | Consider allocating more bandwidth for that computer, or throttling the bandwidth of its peers. |