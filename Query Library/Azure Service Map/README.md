# Azure Service Map Queries

These queries are based on the inventory and dependency data collected by the Service Map solution.

## Prerequisites

Enable Service Map: <https://docs.microsoft.com/en-us/azure/azure-monitor/insights/service-map-configure>

## Remarks

These queries also feature "pretty" column names. This technique allows you to rename column headings with more "friendly" names which support the use of spaces and some special characters.

*Langauge Reference "pretty names": <https://docs.microsoft.com/en-us/azure/kusto/query/schema-entities/entity-names#entity-pretty-names>*

## About Piecharts...

In queries that generate piecharts the "render" operator currently supports only the basic piechart type, so the chart cannot be refined with pre-selected values or chart subtypes (such as *doughnut*) from within the query. I recommend editing the chart to your liking before saving or pinning the view to maximize the utility and impact of the visualization.
