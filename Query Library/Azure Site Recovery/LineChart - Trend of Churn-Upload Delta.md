## LineChart: Trend of Churn-Upload Delta

```
// LineChart: Trend of Churn-Upload Delta
AzureDiagnostics
| where Category == "AzureSiteRecoveryProtectedDiskDataChurn"
| summarize DataChurnKB = avg(toint(Value_s)/1024) by TimeGenerated, InstanceName_s, Resource, ResourceGroup
| join kind = leftouter (
  AzureDiagnostics
  | where Category == "AzureSiteRecoveryReplicationDataUploadRate"
  | summarize DataUploadKB = avg(toint(Value_s)/1024) by TimeGenerated, InstanceName_s, Resource, ResourceGroup
) on TimeGenerated
| extend ComputerName = extract("(.*?):",1, InstanceName_s)
| extend VaultName = Resource
| extend VaultResourceGroup = ResourceGroup
| summarize ["Churn Minus Upload Delta (KB)"] = sum(DataChurnKB-DataUploadKB) by TimeGenerated, ComputerName, VaultName, VaultResourceGroup
| render timechart
```

### What are the key metrics?

**Protected Disk Data Churn** is the rate of change in data volume written to a computer's local disk (how much data is written in a given time period), measured in Bytes. This is converted to KB in the query.

**Replication Data Upload Rate** is the rate of change in data volume uploaded to a Recovery Vault (how much data is sent in a given time period), measured in Bytes. This is converted to KB in the query.

The query calculates the delta between them using the formula:

```Delta = Average Disk Data Churn KB - Replication Data Upload Rate KB```

The Delta value is plotted in a line chart measured over time (timechart type), indicating the efficiency of the the replication process and general stability of the environment required for replication.

### Why is this useful?

The Delta value should normalize near or at zero over time under normal conditions:

+ Positive values indicate that the local disk is writing more data than the Site Recovery Agent is able to transmit to the Recovery Vault.

+ Negative values indicate that the Site Recovery Agent is "catching-up" as it transmits more data than is being written to the local disk.

The occasional positive spike in the Delta should not be cause for alarm, but a sustained or increasing positive value could be caused by one or more of the following issues:

| Possible Issue | What to Investigate |
| --- | --- | 
| Network communication to the Recovery Vault is blocked or bandwidth is constrained. | Verify there are no firewalls blocking access or routers redirecting traffic, and review any bandwidth throttling or allocation rules. |
| The application or connected client activity is overwhelming the local disk. | Verify that local disk activity is within expected operational parameters. |
| The storage layer underpinning the Recovery vault is slower than your infrastructure requires. | Consider upgrading to Premium Storage. |
