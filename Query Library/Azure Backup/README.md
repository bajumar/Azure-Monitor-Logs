# Azure Backup Queries

These queries are based on the data collected from Recovery Vault diagnostic logs.

## Prerequisites

Enable Recovery Vault Diagnostic Log Forwarding: <https://azure.microsoft.com/blog/oms-monitoring-solution-for-azure-backup-using-azure-log-analytics>

Optionally, add the Azure Backup Solution: <https://azure.microsoft.com/en-gb/resources/templates/101-backup-oms-monitoring>


## About Piecharts...

In queries that generate piecharts the "render" operator currently supports only the basic piechart type, so the chart cannot be refined with pre-selected values or chart subtypes (such as *doughnut*) from within the query. I recommend editing the chart to your liking before saving or pinning the view to maximize the utility and impact of the visualization.

## Remarks

*Azure Backup Log Schema Reference - <https://docs.microsoft.com/azure/backup/backup-azure-log-analytics-data-model>*
