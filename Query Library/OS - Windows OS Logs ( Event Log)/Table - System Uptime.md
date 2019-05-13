### Table: System Uptime

```
// Table: System Uptime
Event
| where EventLog == "System" and Source == "EventLog" and EventLevelName == "Information"
| where EventID == "6013"
| summarize arg_max(TimeGenerated, *) by Computer
| extend InSeconds = extract("The system uptime is (.*?) seconds.", 1, RenderedDescription, typeof(double))
| extend Days = toint(InSeconds/60/60/24)
| extend Hours = toint((InSeconds/60/60)-(Days*24))
| extend Minutes = toint((InSeconds/60)-(Days*24*60)-(Hours*60))
| extend Seconds = toint(InSeconds-(Days*24*60*60)-(Hours*60*60)-(Minutes*60))
| project Computer, InSeconds , Days, Hours, Minutes, Seconds
| sort by Computer asc
```