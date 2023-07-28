---
title: Learn about Direct Lake in Power BI and Microsoft Fabric
description: Describes using Direct Lake to analyze very large datasets in Power BI and Microsoft Fabric.
author: minewiskan
ms.author: owend
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-premium
ms.topic: conceptual
ms.date: 05/16/2023
LocalizationGroup: Admin
---
# Direct Lake (PREVIEW)

> [!IMPORTANT]
> Direct Lake is currently in **PREVIEW**. This information relates to a prerelease product that may be substantially modified before it's released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here. Before testing in your environment, be sure to read [Known issues and limitations](#known-issues-and-limitations) later in this article.

*Direct Lake* mode is a groundbreaking new dataset capability for analyzing very large data volumes in Power BI. Direct Lake is based on loading parquet-formatted files directly from a data lake without having to query a Lakehouse endpoint, and without having to import or duplicate data into a Power BI dataset. Direct Lake is a fast-path to load the data from the lake straight into the Power BI engine, ready for analysis. The following diagram shows how classic import and DirectQuery modes compare with the new Direct Lake mode.

:::image type="content" source="media/directlake-overview/directlake-diagram.png" border="false" alt-text="Direct Lake feature diagram.":::

> [!NOTE]
> Data Warehouse is not currently supported in **PREVIEW**.

In DirectQuery mode, the Power BI engine queries the data at the source, which can be slow but avoids having to copy the data. Any changes at the data source are immediately reflected in the query results.

On the other hand, with import mode, performance can be better because the data is cached and optimized for business-intelligence queries without having to query the data source for each DAX query submitted by a report. However, the Power BI engine must first copy the data into the dataset during refresh. Any changes at the source are only picked up with the *next* dataset refresh.

Direct Lake mode eliminates the import requirement by loading the data directly from OneLake. Unlike DirectQuery, there is no translation to other query languages or query execution on other database systems, yielding performance similar to import mode. Because there's no explicit import process, it's possible to pick up any changes at the data source as they occur, combining the advantages of both DirectQuery and import modes while avoiding their disadvantages. Direct Lake mode can be the ideal choice for analyzing very large datasets and datasets with frequent updates at the data source.

## Prerequisites

Direct Lake is supported on Power BI Premium P and Microsoft Fabric F SKUs only. It's not supported on Power BI Pro, Premium Per User, or Power BI Embedded A/EM SKUs.

#### Lakehouse

Before using Direct Lake, you must provision a Lakehouse with one or more delta tables in a workspace hosted on a supported Power BI or Microsoft Fabric capacity. The Lakehouse is required because it provides the storage location for your parquet-formatted files in OneLake. The Lakehouse also provides an access point to launch the Web modeling to create a Direct Lake dataset.

To learn how to provision a Lakehouse, create a delta table in the Lakehouse, and create a dataset for the Lakehouse, see [Create a Lakehouse](#create-a-lakehouse) later in this article.

#### SQL endpoint

As part of provisioning a Lakehouse, a SQL endpoint for SQL querying and a default dataset for reporting are created and updated with any tables added to the Lakehouse. While Direct Lake mode doesn't query the SQL endpoint when loading data directly from OneLake, it's required when a Direct Lake dataset must seamlessly fall back to DirectQuery mode, such as when the data source uses specific features like advanced security or views that can't be read through Direct Lake.

## Known issues and limitations

The following are known issues and limitations during **PREVIEW**:

- Direct Lake size limits are likely to change during **PREVIEW**. More definitive limits will be determined and described in this article by GA (General Availability). If limits are reached, queries are executed in DirectQuery mode. Limits are based on row count per table used by a DAX query. Row counts differ depending on the size of the SKU. To determine if queries fall back to DirectQuery mode, see [Analyze query processing for Direct Lake datasets](directlake-analyze-qp.md).

- You must use the Web modeling experience integrated into Lakehouse to generate Direct Lake datasets. Creating Direct Lake datasets by using Power BI Desktop or XMLA-based automation tools aren't yet supported.

- When generating a Direct Lake dataset in a QSO-enabled workspace, you must sync the dataset manually using the following PowerShell commands with the Power BI Management cmdlets installed (replace WorkspaceID and DatasetID with the GUIDs of your workspace and dataset):

    ```powershell
    Login-PowerBI
    Invoke-PowerBIRestMethod -Url 'groups/WorkspaceId/datasets/DatasetId/sync' -Method Post | ConvertFrom-Json | Format-List
    
    ```

- Calculated columns and calculated tables are not yet supported.

- Some data types may not be supported.

- Only Single Sign-On (SSO) is supported.

- Embedded scenarios that rely on service principals are not yet supported. Direct Lake models use Single Sign-On (SSO).

- The dataset user interface might display a warning icon on a table even though the table has no issues. This will be addressed in a future update.

- The initial, default/auto-generated dataset may not be in Direct Lake mode if there's only a single table in the Lakehouse. To get the dataset to use Direct Lake mode, make a small change on the table in the Lakehouse, like renaming the table. The rename should cause the dataset to switch to Direct Lake mode.
- Tables based TSQL-based views cannot be queried in Direct Lake mode. DAX queries that use these tables fallback to DirectQuery mode.

## Create a Lakehouse

Complete the following steps to create a Lakehouse, a delta table, and a dataset in a Microsoft Fabric or Power BI workspace.

#### To create a Lakehouse

1. In your Microsoft Fabric or Power BI workspace, select **New** > **Show all**, and then in **Data engineering**, select the **Lakehouse** tile.

    :::image type="content" source="media/directlake-overview/directlake-lakehouse-tile.png" border="false" alt-text="Screenshot showing Lakehouse tile.":::

2. In the **New Lakehouse** dialog box, enter a name, and then select **Create**. The name can only contain alphanumeric characters and underscores.

    :::image type="content" source="media/directlake-overview/directlake-new-lakehouse.png" border="false" alt-text="Screenshot showing New Lakehouse dialogue.":::

3. Verify the new Lakehouse is created and opens successfully.

    :::image type="content" source="media/directlake-overview/directlake-verify-lakehouse.png" border="false" alt-text="Screenshot showing verify lakehouse screen.":::

#### Create a delta table in Lakehouse

After creating a new Lakehouse, you must then create at least one delta table so Direct Lake can access some data. Direct Lake can read parquet-formatted files, but for the best performance, it's best to compress the data by using the VORDER compression method. VORDER compresses the data using the Power BI engine’s native compression algorithm. This way the engine can load the data into memory as quickly as possible.

There are multiple options to load data into a Lakehouse, including data pipelines and scripts. The following steps use PySpark to add a delta table to a Lakehouse based on an [Azure Open Dataset](/azure/open-datasets/dataset-catalog).

##### To add a delta table to Lakehouse

1. In the newly created Lakehouse, select **Open notebook**, and then select **New notebook**.

    :::image type="content" source="media/directlake-overview/directlake-lakehouse-new-notebook.png" border="true" alt-text="Screenshot showing new notebook in Lakehouse.":::

1. Copy and paste the following code snippet into the first code cell to let SPARK access the open dataset, and then press **Shift + Enter** to run the code.

    ```python
    # Azure storage access info
    blob_account_name = "azureopendatastorage"
    blob_container_name = "holidaydatacontainer"
    blob_relative_path = "Processed"
    blob_sas_token = r""
    
    # Allow SPARK to read from Blob remotely
    wasbs_path = 'wasbs://%s@%s.blob.core.windows.net/%s' % (blob_container_name, blob_account_name, blob_relative_path)
    spark.conf.set(
      'fs.azure.sas.%s.%s.blob.core.windows.net' % (blob_container_name, blob_account_name),
      blob_sas_token)
    print('Remote blob path: ' + wasbs_path)

    ```

1. Verify the code successfully outputs a remote blob path.

    :::image type="content" source="media/directlake-overview/directlake-remote-blob-path.png" border="false" alt-text="Screenshot showing remote blob path output.":::

1. Copy and paste the following code into the next cell, and then press **Shift + Enter**.

    ```python
    # Read Parquet file into a DataFrame.
    df = spark.read.parquet(wasbs_path)
    print(df.printSchema())

    ```

1. Verify the code successfully outputs the DataFrame schema.

    :::image type="content" source="media/directlake-overview/directlake-dataframe-schema.png" border="false" alt-text="Screenshot showing schema dataframe.":::

1. Copy and paste the following lines into the next cell, and then press **Shift + Enter**. The first instruction enables the VORDER compression method, and the next instruction saves the DataFrame as a delta table in the Lakehouse.

    ```python
    # Save as delta table 
    spark.conf.set("spark.sql.parquet.vorder.enabled", "true")
    df.write.format("delta").saveAsTable("holidays")
    
    ```

1. Verify all SPARK jobs complete successfully. Expand the SPARK jobs list to view more details.

    :::image type="content" source="media/directlake-overview/directlake-spark-jobs-list.png" border="false" alt-text="Screenshot showing Spark jobs list.":::

1. To verify a table has been created successfully, in the upper left area, next to **Tables**, select the ellipsis (**…**), then select **Refresh**, and then expand the **Tables** node.

    :::image type="content" source="media/directlake-overview/directlake-tables-node.png" border="false" alt-text="Screenshot showing Tables node.":::

1. Using either the same method as above or other supported methods, add more delta tables for the data you want to analyze.

##### To create a basic Direct Lake dataset for your Lakehouse

1. In your Lakehouse, select **New dataset**, and then in the **New dataset** dialog, select tables to be included in the dataset.

    :::image type="content" source="media/directlake-overview/directlake-new-dataset.png" border="false"  alt-text="Screenshot showing New dataset.":::

1. Select **Confirm** to generate the Direct Lake dataset. The dataset is automatically saved  in the workspace based on the name of your Lakehouse, and then opens the dataset.

    :::image type="content" source="media/directlake-overview/directlake-open-dataset.png" border="false" alt-text="Screenshot showing open dataset in Power BI.":::

1. Select **Open data model** to open the Web modeling experience where you can add table relationships and DAX measures.

    :::image type="content" source="media/directlake-overview/directlake-web-modeling.png" alt-text="Screenshot showing Web modeling in Power BI.":::

When you're finished adding relationships and DAX measures, you can then create reports, build a composite model, and query the dataset through XMLA endpoints in much the same way as any other dataset. During **PREVIEW**, XMLA write operations are not yet supported.

## Refresh

By default, data changes in OneLake are automatically reflected in a Direct Lake dataset. You can change this behavior by disabling **Keep your Direct Lake data up to date** in the dataset's settings.

:::image type="content" source="media/directlake-overview/direct-lake-refresh.png" alt-text="Direct Lake refresh in dataset settings":::

You may want to disable if, for example, you need to allow completion of data preparation jobs before exposing any new data to consumers of the dataset. When disabled, you can invoke refresh manually or by using the refresh APIs. Invoking a refresh for a Direct Lake dataset is a low cost operation where the dataset analyzes the metadata of the latest version of the Delta Lake table and is updated to reference the latest files in the OneLake.

## Analyze query processing

To determine if a report visual's DAX queries to the data source are providing the best performance by using Direct Lake mode, or falling back to DirectQuery mode, you can use Performance analyzer in Power BI Desktop to analyze queries. To learn more, see [Analyze query processing for Direct Lake datasets](directlake-analyze-qp.md).
