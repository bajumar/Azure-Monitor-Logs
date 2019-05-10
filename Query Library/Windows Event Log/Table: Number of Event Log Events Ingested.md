```
// Table: Number of Event Log Events Ingested
Event
| summarize Events = count() by EventLog, Source
| sort by EventLog asc, Source asc, Events
```
