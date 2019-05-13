### Table: Last Shutdown & Startup

```
// Table: Last Shutdown & Startup
Event
| where EventLog == "System" and Source == "EventLog" and EventLevelName == "Information" or EventLevelName == "Error"
| where EventID == "6006" or EventID == "6008"
| summarize Shutdown = arg_max(TimeGenerated, *) by Computer
| extend State = iff(EventID == "6006", "Clean Shutdown", "Unexpected Shutdown")
| project Computer, State, Shutdown
| join kind = leftouter (
  Event
  | where EventLog == "System" and Source == "EventLog" and EventLevelName == "Information"
  | where EventID == "6005"
  | summarize Startup = arg_max(TimeGenerated, *) by Computer
  | project Computer, Startup
) on Computer
| extend Difference = Startup - Shutdown
|project Computer, State, Shutdown , Startup, Difference
|sort by Computer asc
```