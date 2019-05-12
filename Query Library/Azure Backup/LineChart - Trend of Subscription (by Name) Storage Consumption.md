### LineChart: Trend of Subscription (by Name) Storage Consumption

```
// LineChart: Trend of Subscription (by Name) Storage Consumption
// Replace subscriptionGUID and subscriptionFriendlyName with a valid Subscription GUID and Name, between the quoation marks
let SubscriptionMap = datatable (SubscriptionId: string, SubscriptionName: string)
[
	"subscriptionGUID", "subscriptionFriendlyName",
];
AzureDiagnostics
| where Category == "AzureBackupReport"
| where StorageConsumedInMBs_s != ""
| extend CloudStorageInGB = todouble(StorageConsumedInMBs_s) / 1024
| join kind = leftouter (
	SubscriptionMap
	)  on SubscriptionId
| summarize sum(CloudStorageInGB) by bin(TimeGenerated, 1d), SubscriptionName
| render timechart
```
