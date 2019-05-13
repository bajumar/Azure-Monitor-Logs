### Snippet: RegEx to parse ParameterXml

```
// Snippet: RegEx to parse ParameterXml
| extend Value1 = extract("(<Param>(.*?)</Param>){1}",2,ParameterXml)
| extend Value2 = extract("(<Param>(.*?)</Param>){2}",2,ParameterXml)
| extend Value3 = extract("(<Param>(.*?)</Param>){3}",2,ParameterXml)
```
Add as many lines as needed to extract all of the values in ParameterXml.