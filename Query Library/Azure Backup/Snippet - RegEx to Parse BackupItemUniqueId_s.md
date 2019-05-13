### Snippet: RegEx to parse BackupItemUniqueId_s

```
// Snippet: RegEx to parse BackupItemUniqueId_s
| extend SourceAzureRegion = extract("([^;]+);", 1, BackupItemUniqueId_s)
| extend SourceResourceGroup = extract(".+;(.+);", 1, BackupItemUniqueId_s)
| extend SourceName =  extract("([^;]+$)", 1, BackupItemUniqueId_s)
```