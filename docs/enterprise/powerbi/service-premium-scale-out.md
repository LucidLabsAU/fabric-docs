---
title: Power BI dataset scale-out
description: Learn how Power BI dataset scale-out improves your Power BI performance by reducing dataset query and refresh times
author: KesemSharabi
ms.author: kesharab
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-premium
ms.topic: conceptual
ms.date: 07/25/2023
LocalizationGroup: Premium
---

# Power BI dataset scale-out

> [!IMPORTANT]
> Dataset scale-out is currently in **preview**.

Dataset scale-out helps Power BI deliver fast performance while your reports and dashboards are consumed by a large audience. Dataset scale-out uses your Premium capacity to host one or more read-only *replicas* of your *primary* dataset. By increasing throughput, the read-only replicas ensure performance doesn’t slow down when multiple users submit queries at the same time.

When Power BI creates read-only replicas, it separates them from the primary read-write dataset. The read-only replicas serve Power BI report and dashboard queries, and the read-write dataset is used when write and refresh operations are performed. During write and refresh operations, the read-only replicas continue to serve your reports and dashboard queries without being disrupted. By default, the read-only and read-write datasets are automatically synchronized so that the read-only replicas are kept up-to-date. However, you can disable automatic sync, and choose to synchronize manually at the command line or by script.

The following table shows the required synchronization for each refresh method when Power BI dataset scale-out is *enabled*, and automatic synchronization is *disabled*:

| Refresh method    | Sync                 |
|-------------------|----------------------|
| OnDemand UI       | Always syncs         |
| Scheduled Refresh | Always syncs         |
| Basic REST API    | Manual sync required <sup>[1](#setting)</sup>|
| Advanced REST API | Manual sync required <sup>[1](#setting)</sup>|
| XMLA              | Manual sync required <sup>[1](#setting)</sup>|

<a name="setting">1</a> - With `autoSyncReadOnlyReplicas` in `queryScaleOutSettings` set to false.

## Prerequisites

By default, scale-out is enabled for your tenant, but it's not enabled for datasets in your tenant. To enable scale-out for a dataset, you must use the [Power BI REST APIs](/rest/api/power-bi/datasets/update-dataset-in-group). Before enabling, the following prerequisites must be met:

* The **Scale-out queries for large datasets** setting for your tenant is enabled (default).

* Your workspace resides on a Power BI Premium [capacity](service-premium-what-is.md#capacities-and-skus):
    * Premium Per User (PPU)
    * Power BI Premium P SKUs
    * Power BI A SKUs for Power BI Embedded (also known as [embed for your customers](../developer/embedded/embedded-analytics-power-bi.md#embed-for-your-customers)).
    * Fabric F SKUs

* The [Large dataset storage format](service-premium-large-models.md) setting is enabled.

* To manage datasets by using the REST API, use [Power BI Management cmdlets](/powershell/power-bi/overview?view=powerbi-ps&preserve-view=true). Install by opening PowerShell in Administrator mode, and running the command:

    ```powershell
    Install-Module -Name MicrosoftPowerBIMgmt
    ```

* The following (or higher) app, library, and service versions support connecting to read-only replicas:

    | App, library or service  | Version |
    |--------------------------|---------|
    | Microsoft Analysis Services OLE DB Provider for Microsoft SQL Server (MSOLAP) | 16.0.20.201 (March 2022) |
    | Microsoft.AnalysisServices.AdomdClient (ADOMD.NET) | 19.36.0 (March 2022) |
    | Power BI Desktop         | June 2022 |
    | SQL Server Management Studio (SSMS) | 19.0 |
    | Tabular Editor 2         | 2.16.6   |
    | Tabular Editor 3         | 3.2.3    |
    | DAX Studio               | 3.0.0    |

## Configure scale-out for a dataset

To learn how to enable or disable scale-out for a dataset, or get scale-out status by using PowerShell and the REST APIs, see [Configure dataset scale-out](service-premium-scale-out-configure.md).

## Connect to a specific dataset type

When scale-out is enabled, the following connections are retained:

* By default, Power BI Desktop connects to a read-only replica.

* [Live connection](./../connect-data/desktop-report-lifecycle-datasets.md) reports connect to a read-only replica.

* XMLA client applications connect to the read-write dataset by default.

* Refreshes in the Power BI service and refreshes using the [Enhanced Refresh REST API](./../connect-data/asynchronous-refresh.md) connect to the read-write dataset.

You can connect to a read-only replica or the read-write dataset by appending one of the following strings to the dataset's URL:

* **Read-only** - `?readonly`
* **Read-write** - `?readwrite`

## Disable dataset scale-out for your tenant

Power BI dataset scale-out is enabled by default for a tenant. Power BI tenant admins can disable this setting. To disable dataset scale-out for the tenant, do the following:

1. Go to your [tenant settings](./../admin/service-admin-portal-about-tenant-settings.md).

2. In **Scale-out settings**, expand **Scale-out queries for large datasets**.

3. Toggle the switch to **Disabled**.

4. Select **Apply**.

    :::image type="content" source="media/service-premium-scale-out/disable-scale-out.png" alt-text="A screenshot showing how to disable the scale out tenant settings in the Power BI admin portal.":::

## Considerations and limitations

* Client applications can connect to a read-only replica through the XMLA endpoint, provided they support the mode specified in the connection string. Client applications can also connect to the read-write instance by using the XMLA endpoint.

* Manual and scheduled refreshes are always automatically synchronized with the latest version of the read-only  replicas. REST API refreshes respect the automatic sync configuration. If automatic sync is disabled, your dataset must be synced with the read-only replicas by using the manual sync REST API.

* With automatic sync disabled, XMLA updates and refreshes must be synced with the read-only dataset copies by using the sync REST API.

* When deleting a Power BI scale-out dataset, and creating another dataset with the same name, allow five minutes to pass before creating the new dataset. It might take Power BI a while to remove the replicas of the primary dataset.

* Backup and restore operations are not supported for Power BI scale-out datasets. If you want to restore a dataset, disable scale-out before you restore the dataset. After the restore operation ends, you can enable scale-out again.

* When Power BI dataset scale-out is enabled, changes to the following features, are not supported:
    * Model roles for RLS and OLS
    * Tables that use DirectQuery and Dual data sources

    To make changes to these features, disable scale-out and allow a few minutes for the change to take place before reenabling.

## Next steps

> [!div class="nextstepaction"]
> [Configure dataset scale-out](service-premium-scale-out-configure.md)

> [!div class="nextstepaction"]
> [Tutorial: Test dataset scale-out](service-premium-scale-out-test.md)

> [!div class="nextstepaction"]
> [Synchronize scale-out replicas](service-premium-scale-out-sync-replica.md)

> [!div class="nextstepaction"]
> [Compare dataset scale-out replicas](service-premium-scale-out-app.md)
