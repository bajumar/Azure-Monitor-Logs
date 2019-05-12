### BarChart: Failed Windows Update Attempts

```
// BarChart: Failed Windows Update Attempts
Event
| where EventLog == "System" and Source == "Microsoft-Windows-WindowsUpdateClient" and EventLevelName == "Error"
| extend Description = extract("(<Param>(.*?)</Param>){2}",2,ParameterXml)
| extend UpdateGUID = extract("(<Param>(.*?)</Param>){5}",2,ParameterXml)
| extend KBID = extract(@"KB(\d+)",1,ParameterXml)
| summarize Attempts = count() by Computer, KBID, Description
| render barchart kind = unstacked
```
