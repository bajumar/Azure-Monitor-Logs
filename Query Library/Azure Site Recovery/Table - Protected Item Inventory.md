### Protected Item Inventory

```
// Table: Protected Item Inventory
AzureDiagnostics
| where Category == "AzureSiteRecoveryReplicatedItems"
| summarize hint.strategy=partitioned arg_max(TimeGenerated, *) by name_s
| project name_s, osFamily_s, itemType_s, activeLocation_s, primaryFabricType_s, primaryFabricName_s, recoveryFabricType_s, recoveryFabricName_s, protectionState_s, policyName_s
```