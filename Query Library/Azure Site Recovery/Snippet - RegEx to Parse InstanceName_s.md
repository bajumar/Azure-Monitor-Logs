### Snippet: RegEx to Parse InstanceName_s

```
// Snippet: RegEx to Parse InstanceName_s
| extend ComputerName = extract("(.*?):",1, InstanceName_s)
```
