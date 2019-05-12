# Asset Inventory Queries

These queries are based on the data collected from multiple sources.

## Prerequisites

Enable Service Map: <https://docs.microsoft.com/azure/azure-monitor/insights/service-map-configure>

Enable Performance Data Sources: <https://docs.microsoft.com/azure/azure-monitor/platform/data-sources-performance-counters>

### Linux Performance Counters

```
Any counter starting with "Physical Disk(*)\"
```

### Windows Performance Counters

```
Any counter starting with "LogicalDisk(*)\"
```

## Remarks

The query examples use the "join" operator to correlate data from multiple tables.

*Language Reference "join": <https://docs.microsoft.com/azure/kusto/query/joinoperator>*
