# Asset Inventory Queries

These queries are based on the data collected from multiple sources.

## Prerequisites

Enable Service Map: <https://docs.microsoft.com/azure/azure-monitor/insights/service-map-configure>

Enable Performance Data Sources: <https://docs.microsoft.com/azure/azure-monitor/platform/data-sources-performance-counters>

### Performance Counters Used in the Query Examples

| Query Scenario | Linux | Windows |
| --- | --- | --- |
| Count & Enumerate Disks | Any ```Physical Disk(*)\``` | Any ```LogicalDisk(*)\``` |

## Remarks

The query examples use the "join" operator to correlate data from multiple tables.

*Language Reference "join": <https://docs.microsoft.com/azure/kusto/query/joinoperator>*
