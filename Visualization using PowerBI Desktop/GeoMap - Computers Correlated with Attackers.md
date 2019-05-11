# GeoMap: Computers Correlated with Attackers

![alt text](images/GeoMap%20-%20Computers%20Correlated%20with%20Attackers.PNG "Computers & Attackers")

## Prerequisites

Enable the Azure Wire Data solution: <https://docs.microsoft.com/azure/azure-monitor/insights/wire-data>

## Building the Report

1. In *Azure Monitor Logs*, run the following query using any time interval you wish:

   ```
   // Table: Computers Correlated with Attackers
   WireData
   | where MaliciousIP != "" and Direction == "Inbound"
   | extend ComputerIP = LocalIP
   | extend ComputerPort = LocalPortNumber
   | extend ComputerSubnet = LocalSubnet
   | project ApplicationProtocol, Computer, ComputerIP, ComputerPort, ComputerSubnet, Confidence, IndicatorThreatType, RemoteIP , RemoteIPCountry, RemoteIPLatitude, RemoteIPLongitude, Severity
   | join kind = inner (
     Heartbeat
     | extend ComputerCountry = RemoteIPCountry
     | extend ComputerLatitude = RemoteIPLatitude
     | extend ComputerLongitude = RemoteIPLongitude
     | distinct Computer, ComputerCountry, ComputerEnvironment, ComputerLatitude, ComputerLongitude
   ) on Computer
   | project-away Computer1
   ```

2. Export the query, then copy and paste the exported file contents into *Power BI Desktop*:

   <https://docs.microsoft.com/azure/azure-monitor/platform/powerbi>

   <details>

   <summary>Click here for a summary of the instructions...</summary>

   <p>

   In *Azure Monitor Logs*:

   1. After running a query, in the menu bar select **Export > Power BI Query (M)** to generate a "PowerBIQuery.txt" file.

   2. Open the "PowerBIQuery.txt" text file and copy its contents.

   In *Power BI Desktop*:

   1. In the top menu bar click on the **Get Data** button and choose **Blank Query** to open the *Query Editor* window.

   2. In the *Query Editor* window, from the top menu bar select **Advanced Editor**.

   3. In the *Advanced Editor* window paste the contents of the exported file into the query and click **Done**. You may be prompted for credentials to connect to Azure.

   4. Type in a descriptive name for the query if you wish, then click **Close and Apply** to add the dataset to the report.

   </p>

   </details>

3. In *Power BI Desktop*:

   1. Select the **Map** visualization and drag the following **Fields** to their matching data points:

      | Field | Map Data Point | Note |
      | --- | --- | --- |
      | Computer | Legend | |
      | RemoteIP | Size | Choose *"Count (Distinct)"* for the aggregation. |
      | ComputerLatitude | Latitude | Choose *"Don't summarize"* for the aggregation. |
      | ComputerLongitude | Longitude | Choose *"Don't summarize"* for the aggregation. |

    2. Add a second **Map** visualization and drag the following **Fields** to their matching data points:

       | Field | Map Data Point | Note |
       | --- | --- | --- |
       | RemoteIP | Legend | |
       | Computer | Size | Choose *"Count (Distinct)"* for the aggregation. |
       | RemoteIPLatitude | Latitude | Choose *"Don't summarize"* for the aggregation. |
       | RemoteIPLongitude | Longitude | Choose *"Don't summarize"* for the aggregation. |

     Now you can click on any data point on either map, or in the Legend area of either map, and see the corresponding data points on the other map light up!

     ***Variation 1:*** Change the Size aggregations to *"Count"* if you want to see the total volume of attack attempts instead of unique computer and attacker correlations.

     ***Variation 2:*** Add Slicer and Table controls to make it easier to navigate, and to show more relevant information.

## Closing Remarks

<details>

<summary>Click here to see your reward for diligently reading this document...</summary>

<p>

Here is a shortcut for you!

The Power BI code below is an export of the query example run using a 24-hour time interval. Simply copy and paste the code into Power BI Desktop, then replace the 'WorkspaceID' placeholder in the API URL with a valid Workspace ID to which you have access and you can start creating your report.

```
let AnalyticsQuery =
let Source = Json.Document(Web.Contents("https://api.loganalytics.io/v1/workspaces/'WorkspaceID'/query", 
[Query=[#"query"="WireData
| where MaliciousIP != """" and Direction == ""Inbound""
| extend ComputerIP = LocalIP
| extend ComputerPort = LocalPortNumber
| extend ComputerSubnet = LocalSubnet
| project ApplicationProtocol, Computer, ComputerIP, ComputerPort, ComputerSubnet, Confidence, IndicatorThreatType, RemoteIP , RemoteIPCountry, RemoteIPLatitude, RemoteIPLongitude, Severity
| join kind = leftouter (
Heartbeat
| extend ComputerCountry = RemoteIPCountry 
| extend ComputerLatitude = RemoteIPLatitude 
| extend ComputerLongitude = RemoteIPLongitude 
| distinct Computer, ComputerCountry, ComputerEnvironment, ComputerLatitude, ComputerLongitude
) on Computer
| project-away Computer1
",#"x-ms-app"="OmsAnalyticsPBI",#"timespan"="P1D",#"prefer"="ai.response-thinning=true"],Timeout=#duration(0,0,4,0)])),
TypeMap = #table(
{ "AnalyticsTypes", "Type" }, 
{ 
{ "string",   Text.Type },
{ "int",      Int32.Type },
{ "long",     Int64.Type },
{ "real",     Double.Type },
{ "timespan", Duration.Type },
{ "datetime", DateTimeZone.Type },
{ "bool",     Logical.Type },
{ "guid",     Text.Type },
{ "dynamic",  Text.Type }
}),
DataTable = Source[tables]{0},
Columns = Table.FromRecords(DataTable[columns]),
ColumnsWithType = Table.Join(Columns, {"type"}, TypeMap , {"AnalyticsTypes"}),
Rows = Table.FromRows(DataTable[rows], Columns[name]), 
Table = Table.TransformColumnTypes(Rows, Table.ToList(ColumnsWithType, (c) => { c{0}, c{3}}))
in
Table
in AnalyticsQuery
```

</p>

</details>