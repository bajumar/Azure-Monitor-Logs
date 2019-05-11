# Geographic Map of Computers Correlated with Known Malicious Attackers

![alt text](images/Geographic%20Map%20of%20Computers%20Correlated%20with%20Known%20Malicious%20Attackers.PNG "Computers & Attackers")

1. Run the following query in Azure Monitor Logs:

   ```
   // Table of Computers Correlated with Known Malicious Attackers
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

2. Export the query, then copy and paste the exported file contents into PowerBI Desktop:

   <https://docs.microsoft.com/en-us/azure/azure-monitor/platform/powerbi>

   <details>

   <summary>Click here for a summary of the instructions...</summary>

   <p>

   In *Azure Monitor Logs*:

   1. After running a query, in the menu bar select **Export > Power BI Query (M)** to generate a "PowerBIQuery.txt" file.

   2. Open the "PowerBIQuery.txt" text file and copy its contents.

   In *PowerBI Desktop*:

   1. In the top menu bar click on the **Get Data** button and choose **Blank Query** to open the *Query Editor* window.

   2. In the *Query Editor* window, from the top menu bar select **Advanced Editor**.

   3. In the *Advanced Editor* window paste the contents of the exported file into the query and click **Done**. You may be prompted for credentials to connect to Azure.

   4. Type in a descriptive name for the query if you wish, then click **Close and Apply** to add the dataset to the report.

   5. Create your report. If you wish to publish the report to PowerBI, in the top menu bar click on the **Publish** button.

   </p>

   </details>

3. In *PowerBI Desktop*:

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
