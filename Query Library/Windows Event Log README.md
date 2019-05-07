# Windows Event Log Queries Prerequisites

Enable Windows Event Log Collection - https://docs.microsoft.com/en-us/azure/azure-monitor/platform/data-sources-windows-events

*Be patient as initial schema preparation and data ingestion will take time.*

**Identifying the Required Logs for Queries**

The first "where" filter in each query identifies the required Event Log, Event Source, and Event Level. At a minimum you must add the Event Source and Event Level to be collected for the query to work as intended.
