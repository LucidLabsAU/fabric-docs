---
title: Limitations
description: This article contains a list of current limitations in Microsoft Fabric.
author: joannapea
ms.author: joanpo
ms.reviewer: wiassaf
ms.date: 07/12/2023
ms.topic: conceptual
ms.custom: build-2023
ms.search.form: SQL Endpoint overview, Warehouse overview # This article's title should not change. If so, contact engineering.
---
# Limitations in Microsoft Fabric

**Applies to:** [!INCLUDE[fabric-se-dw](includes/applies-to-version/fabric-se-and-dw.md)]

This article details the current limitations in [!INCLUDE [product-name](../includes/product-name.md)].

[!INCLUDE [preview-note](../includes/preview-note.md)]

## Limitations

Data Warehousing in Microsoft Fabric is currently in preview. The focus of this preview is on providing a rich set of SaaS features and functionality tailored to all skill levels. The preview delivers on the promise of providing a simplified experience through an open data format over a single copy of data. This release is not focused on performance, concurrency, and scale. Additional functionality will build upon the world class, industry-leading performance and concurrency story, and will land incrementally as we progress towards General Availability of data warehousing in [!INCLUDE [product-name](../includes/product-name.md)].

Current general product limitations for Data Warehousing in Microsoft Fabric are listed in this article, with feature level limitations called out in the corresponding feature article.

- <b>IMPORTANT</B> At this time, there's limited T-SQL functionality, and certain T-SQL commands can cause warehouse corruption. See [T-SQL surface area](tsql-surface-area.md) for a list of T-SQL command limitations. 
- Warehouse recovery capabilities are not available during preview.
- Data warehousing is not supported for multiple geographies at this time. Your [!INCLUDE [fabric-dw](includes/fabric-dw.md)] and Lakehouse items should not be moved to a different region during preview.

For more limitations information in specific areas, see:

- [Data types in Microsoft Fabric](data-types.md)
- [Datasets](datasets.md#limitations)
- [Delta lake logs](query-delta-lake-logs.md#limitations)
- [Statistics](statistics.md#limitations)
- [Transactions](transactions.md#limitations)
- [The Visual Query editor](visual-query-editor.md#limitations-with-visual-query-editor)
- [Connectivity](connectivity.md#considerations-and-limitations)
- [Share your Warehouse](share-warehouse-manage-permissions.md#limitations)
- [Tables](tables.md#limitations)

## Limitations of the SQL Endpoint

The following limitations apply to [!INCLUDE [fabric-se](includes/fabric-se.md)] automatic schema generation and metadata discovery.

- Data should be in Delta Parquet format to be auto-discovered in the [!INCLUDE [fabricse](includes/fabric-se.md)]. [Delta Lake is an open-source storage framework](https://delta.io/) that enables building Lakehouse architecture.

- Tables with renamed columns aren't supported in the [!INCLUDE [fabric-se](includes/fabric-se.md)]. 

- Delta tables created outside of the `/tables` folder aren't available in the [!INCLUDE [fabric-se](includes/fabric-se.md)].

   If you don't see a Lakehouse table in the warehouse, check the location of the table. Only the tables that are referencing data in the `/tables` folder are available in the warehouse. The tables that reference data in the `/files` folder in the lake aren't exposed in the [!INCLUDE [fabric-se](includes/fabric-se.md)]. As a workaround, move your data to the `/tables` folder.

- Some columns that exist in the Spark Delta tables might not be available in the tables in the [!INCLUDE [fabric-se](includes/fabric-se.md)]. Refer to the [Data types](data-types.md) for a full list of supported data types. 

- If you add a foreign key constraint between tables in the [!INCLUDE [fabric-se](includes/fabric-se.md)], you won't be able to make any further schema changes (for example, adding the new columns). If you don't see the Delta Lake columns with the types that should be supported in [!INCLUDE [fabric-se](includes/fabric-se.md)], check if there is a foreign key constraint that might prevent updates on the table. 

## Known issues

For known issues in [!INCLUDE [product-name](../includes/product-name.md)], visit [Microsoft Fabric Known Issues](https://support.fabric.microsoft.com/known-issues/).

## Next steps

- [Get Started with Warehouse](create-warehouse.md)