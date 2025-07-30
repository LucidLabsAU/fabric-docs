---
title: Understand the metrics app storage page
description: Learn how to read the Microsoft Fabric Capacity metrics app's storage page.
author: JulCsc
ms.author: juliacawthra
ms.topic: how-to
ms.custom:
ms.date: 03/23/2025
---

# Understand the metrics app storage page

The Microsoft Fabric Capacity Metrics app's storage page provides capacity storage information, showing data for the last 30 days.

## Filters

There are two report filters located at the top of the page and one filter located at top right corner of the table visual.

* **Capacity Name** - Select a capacity. The app displays information related to the selected capacity.

* **Date Range** - Select the date range. The app displays results for the selected date range.

* **Experience** - Select the Fabric experience you want the app to display results for.

* **Storage type** - Select the Fabric storage type you want the app to display results for.

## Cards

In this page, there are three cards present to provide specific information on storage. The information on the cards is filtered according to your capacity and date range selection.

* **Workspaces** -  The total number of workspaces using storage.

* **Current storage (GB)** - Displays the latest storage in GB.

* **Billable storage (GB)** - Displays the billable storage in GB. [Soft-deleted data](../onelake/onelake-disaster-recovery.md#soft-deletion-for-onelake-files) is billed at the same rate as active data.

>[!NOTE]
>* Billable storage volume can be lower than current storage volume. If the capacity has less storage usage at the start of the reporting period, the billable storage volume is lower than the current storage.
>* Current storage can display a zero value. This occurs when the workspaces have not yet begun reporting data for that specific hour.

## Table visual

### Top workspaces by billable storage %

 A table showing storage information for the selected top workspaces. To change the number of workspaces with the largest storage volume you want to review, use the visual *Top* slicer on the visual's filter pane. The workspaces are ordered according to storage volume. The workspaces that have the highest storage volume appear at the top of the list.

* **Workspace name** - Name of the workspace.

* **Workspace ID** - Workspace unique identifier.

* **Operation name** - The name of the displayed operation.

* **Deletion status** - Indicates whether the workspace is active or not. Soft-deleted data is billed at the same rate as active data.

* **Billing type** - Indicates whether the workspace is billable or not.

* **Current storage (GB)** - Current storage in GB of a specific workspace.

* **Billable storage (GB)** -  Billable storage in GB of a specific workspace.

* **Billable storage %** -  Workspace billable storage divided by the sum of billable storages in the capacity. Use to determine the contribution of the workspace to the overall capacity storage use.

## Column charts

There are two column charts in this page showing the storage trend for last 30 days. Both column charts show storage information per day. User can view the hourly distribution by drilling down into a specific day.

### Storage (GB) by date

A column chart that shows average storage in GB by date and hours.

### Cumulative billable storage (GB) by date

A column chart that shows cumulative billable storage by date and hour. Cumulative billable storage is calculated as a sum of billable storage from the start of the selected date time period.

## Export Data

User can export the report's data by selecting Export Data. Selecting Export Data takes you to a page with a matrix visual that displays billable storage details for workspaces in the selected capacity. Hover over the matrix and select 'more options' to export the data.

## Managing large storage capacities

When working with large storage capacities (1TB or more), consider these strategies to maintain control over storage costs and usage:

### Monitoring and alerts for large capacities

- **Set up regular monitoring**: For capacities with high storage usage, review the storage page daily to identify trends and potential issues early.
- **Focus on billable storage percentage**: Pay special attention to workspaces with high billable storage percentages as these drive the majority of your costs.
- **Track storage growth rate**: Monitor the "Storage (GB) by date" chart to identify unusual growth patterns that might indicate data retention issues or unexpected data ingestion.

### Actionable insights for storage optimization

Use the metrics app data to take specific actions:

1. **Identify top storage consumers**: Use the "Top workspaces by billable storage %" table to prioritize optimization efforts on workspaces with the highest impact.
2. **Review deletion status**: Check for soft-deleted workspaces that are still incurring charges and consider permanent deletion if appropriate.
3. **Analyze storage trends**: If cumulative billable storage shows steep increases, investigate recent data ingestion or retention policy changes.

### When storage is out of control

If your storage costs are growing unexpectedly:

1. **Immediate triage**: Sort the workspace table by "Billable storage (GB)" to find the largest consumers.
2. **Check for data retention issues**: Review OneLake data retention policies and identify opportunities to reduce data lifecycle costs.
3. **Investigate sudden increases**: Use the daily storage charts to pinpoint when storage growth accelerated and correlate with business activities.
4. **Consider workspace reorganization**: For workspaces consuming disproportionate storage, evaluate whether data can be archived, moved, or optimized.

### Best practices for large capacity management

- **Implement tiered storage strategies**: Use OneLake's capabilities to manage hot, warm, and cold data appropriately.
- **Regular cleanup processes**: Establish automated or manual processes to clean up unnecessary data and soft-deleted items.
- **Capacity planning**: Use historical growth trends from the metrics app to project future storage needs and budget accordingly.

## Considerations and limitations

[OneLake soft delete](../onelake/onelake-disaster-recovery.md#soft-deletion-for-onelake-files) storage is charged at the same rate as regular storage. For more information about OneLake soft delete, see [OneLake Storage](../onelake/onelake-capacity-consumption.md#onelake-storage).

## Related content

- [Understand the metrics app compute page](metrics-app-compute-page.md)
- [OneLake consumption](/fabric/onelake/onelake-consumption)
- [OneLake capacity consumption example](/fabric/onelake/onelake-capacity-consumption)
