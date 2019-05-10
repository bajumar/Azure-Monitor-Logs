
```
// Table: Most Active Users & Their Activities
AzureActivity
| where Caller has "@"
| summarize Activities = count() by Caller, OperationName
| sort by Activities
```
