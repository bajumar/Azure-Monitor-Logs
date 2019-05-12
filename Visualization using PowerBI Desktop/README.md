# Visualization using Power BI Desktop

In this section you will find examples of relatively simple queries which can be used to create useful interactive reports with dynamic visualizations in Power BI Desktop.

First, get Power BI Desktop for free - <https://powerbi.microsoft.com/desktop>

The specific queries and report creation instructions are provided in each report example, but they all follow the same basic process...

1. In *Azure Monitor Logs*, run your query using any time interval you wish.

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

3. In *Power BI Desktop*, create your report and save it. You can also publish your report to Power BI Server or to Power BI Online if you wish to share it with others in your organization, by clicking on the **Publish** button in the top menu bar.

You can learn more about using Power BI here - <https://docs.microsoft.com/power-bi>