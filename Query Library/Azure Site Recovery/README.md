# Azure Site Recovery Queries

These queries are based on the data collected from Recovery Vault diagnostic logs.

## Prerequisites

Enable Recovery Vault Diagnostic Log Forwarding: <https://docs.microsoft.com/azure/backup/backup-azure-monitoring-use-azuremonitor>

## Snippet Documents

Documents prefixed with *"Snippet"* contain useful re-usable code samples that you can use in your own queries to simplify query creation.

## About Piecharts...

In queries that generate piecharts the "render" operator currently supports only the basic piechart type, so the chart cannot be refined with pre-selected values or chart subtypes (such as *doughnut*) from within the query. I recommend editing the chart to your liking before saving or pinning the view to maximize the utility and impact of the visualization.
