---
title: Direct lake mode and Power BI reporting
description: Learn how to build Power BI reports on top of lakehouse data in Microsoft Fabric 
ms.reviewer: snehagunda
ms.author: tvilutis
author: tedvilutis
ms.topic: conceptual
ms.custom: build-2023
ms.date: 05/23/2023
ms.search.form: Lakehouse PBI Reporting
---

# How direct lake mode works with Power BI reporting

In Microsoft Fabric, when the user creates a lakehouse, the system also provisions the associated SQL endpoint and default dataset. The default dataset is a semantic model with metrics on top of lakehouse data. The dataset allows Power BI to load data for reporting.

[!INCLUDE [preview-note](../includes/preview-note.md)]

When a Power BI report shows an element that uses data, it requests it from the underlying dataset. Next the dataset accesses a lakehouse to retrieve data and return it to the Power BI report. For efficiency default dataset loads commonly requested data into the cache and refreshes it when needed.

Lakehouse applies V-order optimization to tables. This optimization enables quickly loading data into the dataset and having it ready for querying without any other sorting or transformations.

This approach gives unprecedented performance and the ability to instantly load large amounts of data for Power BI reporting.

:::image type="content" source="media\pbi-reporting\dataset.png" alt-text="Screenshot of the default dataset landing page." lightbox="media\pbi-reporting\dataset.png":::

## Setting permissions for report consumption

The default dataset is retrieving data from a lakehouse on demand. To make sure that data is accessible for the user that is viewing Power BI report, necessary permissions on the underlying lakehouse need to be set.

One option is to give the user *Viewer* role in the workspace and grant necessary permissions to data using SQL endpoint security. Alternatively, the user can be given *Admin, Member, or Contributor* role to have full access to the data.

## Next steps

- [Default Power BI datasets in Microsoft Fabric](../data-warehouse/datasets.md)
