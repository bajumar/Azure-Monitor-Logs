# All OS Performance (Cross-Platform) Queries

These queries are based on the data collected from Operating System performance counters.

## Prerequisites

Enable Performance Data Sources: <https://docs.microsoft.com/azure/azure-monitor/platform/data-sources-performance-counters>

### Performance Counters Used in the Query Examples

| Query Scenario | Linux | Windows |
| --- | --- | --- |
| Count CPUs | Any ```Processor(*)\``` | Any ```Processor(*)\``` |
| Count & Enumerate Disks | Any ```Physical Disk(*)\``` | Any ```LogicalDisk(*)\``` |
| Process-Level CPU Utilization | ```Process(*)\Pct User Time``` | ```Process(*)\% Processor Time```|
| | ```Process(*)\Pct Privileged Time``` | |
| Process-Level Memory Utilization | ```Process(*)\Used Memory``` | ```Process(*)\Working Set``` |

