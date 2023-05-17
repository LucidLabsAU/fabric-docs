---
title: Learn how to analyze query processing for Direct Lake datasets
description: Describes how to analyze query processing for Direct Lake datasets.
author: minewiskan
ms.author: owend
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-premium
ms.topic: conceptual
ms.date: 05/16/2023
LocalizationGroup: Admin
---
# Analyze query processing for Direct Lake datasets (PREVIEW)

> [!IMPORTANT]
> Direct Lake is currently in **PREVIEW**. This information relates to a prerelease product that may be substantially modified before it's released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

Power BI datasets in [*Direct Lake*](directlake-overview.md) mode read delta tables directly from OneLake — unless they have to fallback to *DirectQuery* mode. Typical fallback reasons include memory pressures may prevent loading of columns required to process a DAX query, and certain features at the data source might not support Direct Lake mode, like SQL views in a Warehouse. In general, Direct Lake mode provides the best DAX query performance unless a fallback to DirectQuery mode is necessary. Because fallback to DirectQuery mode can impact DAX query performance, it's important to analyze query processing for a Direct Lake dataset to identify if and how often fallbacks occur.

There are several different tools you can use to analyze query processing. Performance analyzer in Power BI Desktop, SQL Server Profiler, and third-party tools like DAX Studio all work well. This article describes using Performance Analyzer for a quick glance, and SQL Profiler for more thorough tracing.

## Analyze by using Performance analyzer

Performance analyzer can provide a quick and easy look into how a visual queries a data source, and how much time it takes to render a result.

1. Start Power BI Desktop. On the startup screen select **Get Data**.

1. In **Get Data** > **Power Platform**, select **Power BI datasets**, and then select **Connect**.

1. In the **Data hub** page, select the Direct Lake dataset you want to connect to, and then select **Connect**.

1. Place a card visual on the report canvas, select a data column to create a basic report, and then on the **View** menu, select **Performance analyzer**.

    :::image type="content" source="media/directlake-analyze-qp/viewing-performance-analyzer.png" alt-text="Viewing Performance analyzer":::

1. In the **Performance analyzer** pane, select **Start recording**.

    :::image type="content" source="media/directlake-analyze-qp/start-recording.png" alt-text="Select Start recording":::

1. In the **Performance analyzer** pane, select **Refresh visuals**, and then expand the Card visual. Note that the Card does not generate any DirectQuery processing. This indicates the dataset was able to process the visual’s DAX queries in Direct Lake mode.

    :::image type="content" source="media/directlake-analyze-qp/refresh-visual-with-table-column.png" alt-text="Refresh visual with table column":::

1. In the **Visualizations** pane, replace the table column with a column from a table based on a Warehouse view to force a fallback to DirectQuery mode.

1. In **Performance analyzer**, note the visual’s queries now take longer and  there are **Direct query** events. This indicates that the dataset is falling back to DirectQuery mode to process the visual’s DAX query.

    :::image type="content" source="media/directlake-analyze-qp/fallback-based-on-view.png" alt-text="Fallback based on view":::

## Analyze by using SQL Server Profiler

SQL Server Profiler can provide more details about query performance by tracing query events. It's installed with [SQL Server Management Studio (SSMS)](/sql/ssms/download-sql-server-management-studio-ssms). Before starting, make sure you have the latest version of SSMS installed.

> [!NOTE]
> Currently, you can only trace query processing for manually created Direct Lake datasets. SQL Server Profiler and other XMLA-based management tools can't connect to default datasets.

1. Start SQL Server Profiler from the Windows menu.

1. In SQL Server Profiler, select **File** > **New Trace**.

1. In **Connect to Server** > **Server type**, select **Analysis Services**, then in **Server name**, enter the URL to your workspace, then select an authentication method, and then enter a username to sign in to the workspace.

    :::image type="content" source="media/directlake-analyze-qp/sql-profiler-connect-server.png" alt-text="Connect to server dialog":::

1. Select **Options**. In **Connect to database**, enter the name of your dataset and then select **Connect**. Sign in to Azure Active Directory.

    :::image type="content" source="media/directlake-analyze-qp/sql-profiler-connect-enter-dataset.png" alt-text="Enter dataset":::

1. In **Trace Properties** > **Events Selection**, select the **Show all events** checkbox.

    :::image type="content" source="media/directlake-analyze-qp/sql-profiler-show-all-events.png" alt-text="Events selection - Show all events":::

1. Scroll to **Query Processing**, and then select checkboxes for the following events:

    |Event  |Description  |
    |---------|---------|
    |**DirectQuery_Begin**</BR>**DirectQuery_End**     |   If DirectQuery Begin/End events appear in the trace, the dataset might have fallen back to DirectQuery mode. Note, however, that the presence of EngineEdition queries and possibly queries to check Object Level Security (OLS) do not represent a fallback because the engine always uses DirectQuery mode for these non-query processing related checks.        |
    |**VertiPaq_SE_Query_Begin**</BR> **VertiPaq_SE_Query_Cache_Match**</BR> **VertiPaq_SE_Query_Cache_Miss**</BR> **VertiPaq_SE_Query_End**     |  VertiPaq storage engine (SE) events in Direct Lake mode are the same as for import mode.      |

    It should look like this:

    :::image type="content" source="media/directlake-analyze-qp/sql-profiler-select-events.png" alt-text="Image showing select query processing events in SQL Server Profiler":::

1. Select **Run**. In Power BI Desktop, create a new report or interact with an existing report to generate query events. Review the SQL Server Profiler trace report for query processing events.

    The following image shows an example of query processing events for a DAX query. In this trace, the VertiPaq storage engine (SE) events indicate that the query was processed in Direct Lake mode.
    :::image type="content" source="media/directlake-analyze-qp/sql-profiler-qp-events.png" alt-text="Query processing events in SQL Server Profiler":::

## See also

[Direct Lake](directlake-overview.md)