# GeoMap: Computer Geo-Locations

![alt text](images/GeoMap%20-%20Computer%20Geo-Locations.PNG "Computer Geo-Locations")

## Prerequisites

Install the Agent: <https://docs.microsoft.com/azure/azure-monitor/platform/log-analytics-agent>

## Building the Report

1. In *Azure Monitor Logs*, run the following query using any time interval you wish:

   ```
   // Table: Computer Geo-Locations
   Heartbeat
   | distinct Computer, ComputerEnvironment, RemoteIPCountry, RemoteIPLatitude, RemoteIPLongitude
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

3. In *Power BI Desktop*, select the **Map** visualization and drag the following **Fields** to their matching data points:

   | Field | Map Data Point | Note |
   | --- | --- | --- |
   | Computer | Size | |
   | ComputerEnvironment | Legend | |
   | RemoteIPLatitude | Latitude | Choose *"Don't summarize"* for the aggregation. |
   | RemoteIPLongitude | Longitude | Choose *"Don't summarize"* for the aggregation. |

   ***Variation 1:*** If you would like to see the Computer Names in each location, instead of the Environment Name, drag the *Computer* field to the *Legend* data point.

   ***Variation 2:*** If you prefer a simplified Country-level view you can drag the *RemoteIPCountry* field to the *Location* data point, however you cannot have both the *Location* and the combination of *Lat/Long* data points populated simultaneously.

## Closing Remarks

<details>

<summary>Click here to see your reward for diligently reading this document...</summary>

<p>

Here is a shortcut for you!

The Power BI code below is an export of the query example run using a 24-hour time interval. Simply copy and paste the code into Power BI Desktop, then replace the 'WorkspaceID' placeholder in the API URL with a valid Workspace ID to which you have access and you can start creating your report.

```
let AnalyticsQuery =
let Source = Json.Document(Web.Contents("https://api.loganalytics.io/v1/workspaces/'WorkspaceID'/query", 
[Query=[#"query"=" 
   Heartbeat
   | distinct Computer, ComputerEnvironment, RemoteIPCountry, RemoteIPLatitude, RemoteIPLongitude",#"x-ms-app"="OmsAnalyticsPBI",#"timespan"="P1D",#"prefer"="ai.response-thinning=true"],Timeout=#duration(0,0,4,0)])),
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