### Table: User-Initiated Shutdowns

```
// Table: User-Initiated Shutdowns
Event
| where EventLog == "System" and Source == "User32" and EventLevelName == "Information"
| where EventID == "1074"
| extend Process = extract("(<Param>(.*?)</Param>){1}",2,ParameterXml)
| extend Name = extract("(<Param>(.*?)</Param>){2}",2,ParameterXml)
| extend Reason = extract("(<Param>(.*?)</Param>){3}",2,ParameterXml)
| extend ReasonCode = extract("(<Param>(.*?)</Param>){4}",2,ParameterXml)
| extend ShutdownType = extract("(<Param>(.*?)</Param>){5}",2,ParameterXml)
| extend Comment = extract("(<Param>(.*?)</Param>){6}",2,ParameterXml)
| extend UserID = extract("(<Param>(.*?)</Param>){7}",2,ParameterXml)
| project Computer, TimeGenerated, ShutdownType, UserID, Process, Reason, Comment
| sort by Computer asc
```
