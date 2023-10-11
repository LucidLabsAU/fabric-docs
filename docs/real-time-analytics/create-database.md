---
title: Create a KQL database
description: Learn how to create a KQL database in Real-Time Analytics.
ms.reviewer: tzgitlin
ms.author: yaschust
author: YaelSchuster
ms.topic: how-to
ms.custom: build-2023
ms.date: 09/28/2023
ms.search.form: KQL Database
---
# Create a KQL database

[!INCLUDE [preview-note](../includes/preview-note.md)]

In Real-Time Analytics, you interact with your data in the context of databases. A single workspace can hold multiple databases, and each database can hold multiple tables.

In this article, you learn how to create a new KQL database. Once your KQL database has data, you can proceed to query your data using Kusto Query Language in a KQL queryset.

## Prerequisites

* A [workspace](../get-started/create-workspaces.md) with a Microsoft Fabric-enabled [capacity](../enterprise/licenses.md#capacity)

## Create a new KQL database

1. Select **New** > **KQL Database**.

    :::image type="content" source="media/database-editor/create-database.png" alt-text="Screenshot of Real-time Analytics workspace that shows the dropdown menu of the ribbon button titled New. Both the New tab and the entry titled KQL Database are highlighted.":::

1. Enter your database name, then select **Create**.

    > [!NOTE]
    > The database name can contain alphanumeric characters, underscores, periods, and hyphens. Special characters aren't supported.

    :::image type="content" source="media/create-database/new-database.png" alt-text="Screenshot of the New KQL Database window showing the database name. The Create button is highlighted.":::

The KQL database has now been created within the context of the selected workspace.

## Database details

The main page of your KQL database shows an overview of the contents in your database. The following table lists the available information.

:::image type="content" source="media/create-database/database-dashboard.png" alt-text="Screenshot of KQL database main page showing the database details cards."  lightbox="media/create-database/database-dashboard.png":::

|Card | Item| Description|
|---|---|---|
|**Database details**|
| | Created by | User name of person who created the database.|
| | Region | Shows the region of the data and services.|
| | Created on | Date of database creation.|
| | Last ingestion | Date on which data was ingested last into the database.|
| | Query URI | URI that can be used to run queries or to store management commands.|
| | Ingestion URI | URI that can be used to get data.|
| | OneLake folder | OneLake folder path that can be used for creating shortcuts. You can also activate and deactivate data copy to OneLake.|
| **Size**|
| | Compressed| Total size of compressed data.|
| | Original size | Total size of uncompressed data.|
| | Compression ratio | Compression ratio of the data.|
|**Top tables**|  
| | Name | Lists the names of tables in your database. Select a table to see more information.|
| | Size | Database size in megabytes. The tables are listed in a descending order according to the data size.|
|**Most active users**|
| | Name | User name of most active users in the database.|
| | Queries run last month | The number of queries run per user in the last month.|
|**Recently updated functions**|
| | |  Lists the function name and the time it was last updated.|
|**Recently used Querysets**|
| | | Lists the recently used KQL queryset and the time it was last accessed.|
|**Recently created Data streams**|
| | | Lists the data stream and the time it was created.|

## Related content

* [Get data from a blob](get-data-blob.md)
* [Get data from Amazon S3](get-data-amazon-s3.md)
* [Get data from Azure Event Hubs](get-data-event-hub.md)
* [Get data from OneLake](get-data-onelake.md)
