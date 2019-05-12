### Table: Number of Syslog Events Ingested

```
// Table: Number of Syslog Events Ingested
Syslog
| summarize Events = count() by Facility, ProcessName
| sort by Facility asc, ProcessName asc, Events
```
