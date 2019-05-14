### Snippet: JSON to Parse replicationHealthErrors_s

```
// Snippet: JSON to Parse replicationHealthErrors_s
| mvexpand d = parsejson(replicationHealthErrors_s)
| extend errorCategory = tostring(d.errorCategory)
| extend errorCode = tostring(d.errorCode)
| extend errorLevel = tostring(d.errorLevel)
| extend errorMessage = tostring(d.errorMessage)
| extend creationTime = tostring(d.creationTime)
| extend possibleCauses = tostring(d.possibleCauses)
| extend recommendation = tostring(d.recommendation)
```
