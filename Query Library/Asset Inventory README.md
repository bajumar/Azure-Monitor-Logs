# Asset Inventory Queries Prerequisites & Comments

The queries in this category are focused on basic Asset Inventory, retrieving data such as Operating System versions, Proccessor counts, Memory and Disk allocation, etc. The quality of the results from these queries depend on the solutions that are enabled, so I will be including several examples based on various solutions and solution combinations. In particular, the Service Map solution will collect the most relevant data for creating effective queries in this category.

**About Piecharts...**

In queries that generate piecharts the "render" operator currently supports only the basic piechart type, so the chart cannot be refined with pre-selected values or chart subtypes (such as *doughnut*) from within the query. I recommend editing the chart to your liking before saving or pinning the view to maximize the utility and impact of the vizualization.

**Heartbeat-based Query Examples**

If you are only able to leverage Heartbeat data note that the Heartbeat logs for Windows Servers do not log the full operating system release name (e.g. Windows Server 2019), so the full release name must be derived from the operating system Major and Minor version numbers. Windows operating system version numbers are identical for Windows Servers and Windows Dekstops from the same release cycle (e.g. Windows 10 version is identified as "10.0", and Windows Server 2016 version is also identified as "10.0").

The relevant queries in this repo assume that the logged version numbers are for Windows Server oprating systems, and use the Azure Monitor Logs Query Language "datatable" operator to construct the lookup table for mapping the version numbers to the equivalent full release names. Your results will be more accurate if you leverage other solutions to retrieve the full release name of the operating system.

*Reference: https://docs.microsoft.com/en-us/windows/desktop/SysInfo/operating-system-version*

**ServiceMap-based Query Examples**

Servce Map collects a richer dataset, including Azure-specific configuration information such as VM Size and Region, so the construction of relevant queries is much simpler. The queries in this section also feature "pretty" column names, which support the use of spaces and special characters.

Enable Service Map - https://docs.microsoft.com/en-us/azure/azure-monitor/insights/service-map-configure

*Entity pretty names: https://docs.microsoft.com/en-us/azure/kusto/query/schema-entities/entity-names#entity-pretty-names*

**Perf-based Query Examples**

Enabling performance counter data collection supports the ability to derive, or calculate, additional "hardware" inventory information. The required performance counters are specified in the comments header of each query example. Whenever possible, the query examples will leverage the minimum recommended set of performance counters for Windows and Linux which are identified when performance data collection is initially configured. 

Enable Performance Data Sources - https://docs.microsoft.com/en-us/azure/azure-monitor/platform/data-sources-performance-counters
