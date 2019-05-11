# Azure Agent (Heartbeat) Queries

These queries are based on the data retrieved with the Agent Heartbeat.

## Prerequisites

None.

## Using Heartbeat Data to Inventory Windows Server Versions

The Heartbeat logs for Windows Servers do not log the Operating System release name (e.g. Windows Server 2019), so the release name must be derived from the logged Major and Minor version numbers. Windows operating system version numbers are identical for Windows Server and Windows Client Operating Systems from the same release cycle (e.g.  Windows Server 2016 version number is "10.0", and Windows 10 version number is also "10.0").

*Windows Version Reference: <https://docs.microsoft.com/windows/desktop/SysInfo/operating-system-version>*

These queries assume that the logged version numbers are for Windows Server, and use the "datatable" operator to construct the lookup table for mapping the version numbers to the equivalent full release names.

*Language Reference "datatable": <https://docs.microsoft.com/azure/kusto/query/datatableoperator>*

## About Piecharts...

In queries that generate piecharts the "render" operator currently supports only the basic piechart type, so the chart cannot be refined with pre-selected values or chart subtypes (such as *doughnut*) from within the query. I recommend editing the chart to your liking before saving or pinning the view to maximize the utility and impact of the visualization.
