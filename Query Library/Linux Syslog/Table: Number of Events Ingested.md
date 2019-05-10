```
// Table: Number of Events Ingested
Syslog
| summarize Events = count() by Facility, ProcessName
| sort by Facility asc, ProcessName asc, Events
```