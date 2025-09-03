---
title: What is the Microsoft Fabric Capacity Metrics app?
description: Learn how to evaluate your Microsoft Fabric capacity's health, by reading the metrics app.
author: julcsc
ms.author: juliacawthra
ms.topic: conceptual
ms.custom:
ms.date: 06/19/2025
---

# What is the Microsoft Fabric Capacity Metrics app?

> [!NOTE]
> The Microsoft Fabric Capacity Metrics app has been updated to include support for both EM/A and P SKUs.

Fabric resides on a capacity which is a pool of resources allocated to your platform. Each capacity has its own number of [Capacity Units (CUs)](licenses.md). CUs are used to measure the compute power available for your capacity.

The Microsoft Fabric Capacity Metrics app is designed to provide monitoring capabilities for Microsoft Fabric capacities. Use the app to monitor your capacity consumption and make informed decisions on how to use your capacity resources. For example, the app can help identify when to scale up your capacity or when to turn on [autoscale](/power-bi/enterprise/service-premium-auto-scale).

The app provides comprehensive insights for cost and storage management, especially important for large capacities where costs can quickly spiral out of control. Key capabilities include:

- **Cost visibility**: Track which workspaces, users, and operations are driving the highest costs through CU consumption patterns
- **Storage optimization**: Monitor storage growth trends and identify opportunities to reduce billable storage usage
- **Performance insights**: Understand how capacity utilization affects user experience and identify optimization opportunities
- **Capacity planning**: Use historical data to make informed decisions about scaling and resource allocation

The app is updated often with new features and functionalities and provides the most in-depth information into how your capacities are performing.

## Install the app

You must be a capacity admin to install and view the Microsoft Fabric Capacity Metrics app.

To install the app, follow the instructions in [Install the Microsoft Fabric Capacity Metrics app](metrics-app-install.md).

## Interpreting insights for cost and storage control

When capacity costs or storage usage are concerning, use these approaches to extract actionable insights from the metrics app:

### Identifying cost overruns

1. **Review the [compute page](metrics-app-compute-page.md)**: Look for consistently high utilization percentages or frequent throttling events that indicate oversized operations or insufficient capacity.

2. **Analyze the [matrix by item and operation](metrics-app-compute-page.md#matrix-by-item-and-operation)**: Sort by "CU (s)" to identify the highest resource consumers. Focus optimization efforts on these items first.

3. **Check [performance delta](metrics-app-calculations.md#performance-delta)**: Items showing negative performance delta (red or orange) may be becoming less efficient and driving increased costs.

### Storage growth analysis

1. **Monitor [storage trends](metrics-app-storage-page.md)**: Watch for sudden increases in the "Cumulative billable storage (GB) by date" chart that indicate unexpected data growth.

2. **Identify storage hotspots**: Use the "Top workspaces by billable storage %" table to focus cleanup efforts on the highest-impact areas.

3. **Review billing patterns**: Compare "Current storage (GB)" with "Billable storage (GB)" to understand your cost exposure and identify opportunities for data lifecycle optimization.

### Emergency response using metrics

When immediate action is needed:

1. **Throttling alerts**: If background rejection shows >100%, all requests are being rejected. Use the [calculation formulas](metrics-app-calculations.md#calculate-the-time-to-recover-from-throttling) to estimate recovery time.

2. **Capacity overload**: Interactive rejection >100% means user requests are failing. Consider immediate capacity scaling or workload redistribution.

3. **Storage intervention**: Rapidly increasing billable storage may require immediate investigation of data ingestion processes or retention policies.

For comprehensive cost management strategies, see [Evaluate and optimize your Microsoft Fabric capacity](optimize-capacity.md).

## Considerations and limitations

When using the Microsoft Fabric Capacity Metrics app, consider the following considerations and limitations:

- The report doesn't show application IDs.
- To hide user emails in the app, disable the [Show user data in the Fabric Capacity Metrics app and reports](../admin/service-admin-portal-audit-usage.md#show-user-data-in-the-fabric-capacity-metrics-app-and-reports) setting in the Admin portal.
- Billable items and operations consume CU units from your capacity and are paid for by your organization. Non-billable items and operations reflect preview features that don't count towards your capacity limit, and aren't paid for. They provide an indication of possible future impact on your capacity. When preview features become generally available, your organization starts paying for them and their impact on your capacity is taking into account.
- In the [Capacity utilization and throttling](metrics-app-compute-page.md#capacity-utilization-and-throttling) visual logarithmic's view, the primary axis seen on the left of the visual, isn't aligned with the secondary axis seen on the right of the visual.
- In the [interactive](metrics-app-timepoint-page.md#interactive-operations-for-timerange) and [background](metrics-app-timepoint-page.md#background-operations-for-timerange) operation tables, the *Throttling(s)* column displays zero when throttling is disabled, even when the capacity is overloaded.
- There's a difference of 0.01-0.05 percent between the *CU %* value in the [Top row visuals](metrics-app-timepoint-page.md#top-row-visuals) *Heartbeat line chart*, and the [interactive](metrics-app-timepoint-page.md#interactive-operations-for-timerange) and [background](metrics-app-timepoint-page.md#background-operations-for-timerange) operations tables *Total CU* values.
- When the capacity state remains unchanged during the selected dates or the past 14 days, it won't appear in the System Event table.
- Updates from version 1 to version 1.1 are installed in a new workspace.
- Sampling might occur while exporting data from the Export Data page. See second and third bullet in [Considerations and limitations](/power-bi/visuals/power-bi-visualization-export-data?tabs=powerbi-desktop#considerations-and-limitations).
- The semantic model used by the Microsoft Fabric Capacity Metrics application is only supported for use by the reports provided in the application. Any consumption from, usage of, or modification of the semantic model is not supported.
- The cumulative consumption of CU seconds for a specific item over the past 14 days is displayed in the *CU (s)* column of the [matrix by item and operation](metrics-app-compute-page.md#matrix-by-item-and-operation) table. If the item was moved from another workspace to the current workspace in the last 14 days, the cumulative consumption of CU seconds for the item in the previous workspace is included in the *CU (s)* column.
- The Microsoft Fabric Capacity Metrics app doesn't support environments that use [private links](../security/security-private-links-overview.md).
- The threshold values on throttling visuals don't reflect applied surge protection settings. To view the actual [surge protection](surge-protection.md) thresholds, refer to the Admin Portal in the Power BI service.

## Related content

- [Install the Microsoft Fabric Capacity Metrics app](metrics-app-install.md)
