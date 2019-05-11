# Azure Backup Queries Prerequisites
	
1. Configure your Recovery Vault(s) to send Diagnostic Logs to your Log Analytics Workspace - <https://azure.microsoft.com/en-us/blog/oms-monitoring-solution-for-azure-backup-using-azure-log-analytics>

2. Add the Azure Backup Solution to your Log Analytics Workspace - <https://azure.microsoft.com/en-gb/resources/templates/101-backup-oms-monitoring>

*Be patient as initial schema preparation and data ingestion will take time.*

*Log Schema Reference - <https://docs.microsoft.com/en-us/azure/backup/backup-azure-log-analytics-data-model>*

### About Piecharts...

In queries that generate piecharts the "render" operator currently supports only the basic piechart type, so the chart cannot be refined with pre-selected values or chart subtypes (such as *doughnut*) from within the query. I recommend editing the chart to your liking before saving or pinning the view to maximize the utility and impact of the visualization.

