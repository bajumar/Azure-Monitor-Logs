### Table: Users Attempting Unauthorized Activities

```
// Table: Users Attempting Unauthorized Activities
AzureActivity
| where ActivitySubstatus == "Unauthorized" and Caller has "@"
| extend eventProperties = parse_json(Properties)
| extend eventStatus = tostring(parse_json(eventProperties.statusMessage))
| extend Reason = extractjson("$.error.message", eventStatus)
| project Reason, Caller, CallerIpAddress, OperationName , ResourceGroup, EventSubmissionTimestamp
| sort by Reason asc, Caller asc
```
