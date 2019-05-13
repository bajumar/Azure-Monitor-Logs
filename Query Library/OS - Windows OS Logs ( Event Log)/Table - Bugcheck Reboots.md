### Table: Bugcheck Reboots

```
// Table: Bugcheck Reboots
Event
| where EventLog == "System" and Source == "Microsoft-Windows-WER-SystemErrorReporting" and EventLevelName == "Error"
| where EventID == "1001"
| extend Bugcheck = extract("(<Param>(.*?)</Param>){1}",2,ParameterXml)
| extend DumpFile = extract("(<Param>(.*?)</Param>){2}",2,ParameterXml)
| extend ReportID = extract("(<Param>(.*?)</Param>){3}",2,ParameterXml)
| project Computer, TimeGenerated, Bugcheck, DumpFile, ReportID
| sort by Computer asc
```
