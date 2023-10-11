---
title: Data warehouse billing and utilization reporting
description: Learn more about utilization reporting for the data warehouse, including capacity and compute usage reporting.
author: sowmi93
ms.author: sosivara
ms.reviewer: wiassaf
ms.date: 10/01/2023
ms.topic: conceptual
ms.search.form: Warehouse billing and utilization
---

# Billing and utilization reporting in Synapse Data Warehouse

**Applies to:** [!INCLUDE[fabric-se-and-dw](includes/applies-to-version/fabric-se-and-dw.md)]

The article explains compute usage reporting of the Synapse Data Warehouse in [!INCLUDE [product-name](../includes/product-name.md)], which includes read and write activity against the Warehouse, and read activity on the SQL Endpoint of the Lakehouse.

When you use a Fabric capacity, your usage charges appear in the Azure portal under your subscription in [Microsoft Cost Management](/azure/cost-management-billing/cost-management-billing-overview). To understand your Fabric billing, visit [Understand your Azure bill on a Fabric capacity](../enterprise/azure-billing.md).

## Capacity

In Fabric, based on the Capacity SKU purchased, you're entitled to a set of Capacity Units (CUs) that are shared across all Fabric workloads. For more information on licenses supported, see [Microsoft Fabric licenses](/fabric/enterprise/licenses).

Capacity is a dedicated set of resources that is available at a given time to be used. Capacity defines the ability of a resource to perform an activity or to produce output. Different resources consume CUs at different times.

### Capacity in Fabric Synapse Data Warehouse

In the capacity-based SaaS model, Fabric data warehousing aims to make the most of the purchased capacity and provide visibility into usage.

CUs consumed by data warehousing include read and write activity against the Warehouse, and read activity on the SQL Endpoint of the Lakehouse.

The "CPU time" metric captures usage of compute resources when requests are executed. "CPU time" isn't the same as elapsed time, it's the time spent by compute cores in execution of a request. Similar to how Windows accounts for Processor Time, multi-threaded workloads record more than one second of "CPU time" per second.

## Compute usage reporting

The [Microsoft Fabric Capacity Metrics app](../enterprise/metrics-app.md) provides visibility into capacity usage for all Fabric workloads in one place. It's mostly used by capacity administrators to monitor the performance of workloads and their usage, compared to purchased capacity.  

Once you have installed the app, select the **Warehouse** from the **Select item kind:** dropdown list. The **Multi metric ribbon chart** chart and the **Items (14 days)** data table now show only **Warehouse** activity.

:::image type="content" source="media/usage-reporting/fabric-capacity-metrics-app.gif" alt-text="An animated gif of the Fabric Capacity Metrics Overview page in the Microsoft Fabric Capacity Metrics app." lightbox="media/usage-reporting/fabric-capacity-metrics-app.gif":::

### Warehouse operation categories

You can analyze universal compute capacity usage by workload category, across the tenant. Usage is tracked by total Capacity Unit Seconds (CU(s)). The table displayed shows aggregated usage across the last 14 days.

Both the Warehouse and SQL Endpoint roll up under **Warehouse** in the Metrics app, as they both use SQL compute. The operation categories seen in this view are:

- **Warehouse Query**: Compute charge for all user generated and system generated T-SQL statements within a warehouse.
- **SQL Endpoint Query**: Compute charge for all user generated and system generated T-SQL statements within a SQL Endpoint.
- **OneLake Compute**: Compute charge for all reads and writes for data stored in OneLake.

For example:

:::image type="content" source="media/usage-reporting/warehouse-operations.png" alt-text="A screenshot of the Data warehouse operation categories in the Microsoft Fabric Capacity Metrics app." lightbox="media/usage-reporting/warehouse-operations.png":::

### Timepoint explore graph

This graph in the Microsoft Fabric Capacity Metrics app shows utilization of resources compared to capacity purchased. 100% of utilization represents the full throughput of a capacity SKU and is shared by all Fabric experiences. This is represented by the yellow dotted line. The **Logarithmic** scale option enables the **Explore** button, which opens a detailed drill through page.

In general, similar to Power BI, [operations are classified either as *interactive* or *background*](/power-bi/enterprise/service-premium-interactive-background-operations#operation-list), and denoted by color. All operations in **Warehouse** category are reported as *background* to take advantage of 24 hour smoothing of activity to allow for the most flexible usage patterns. Classifying all data warehousing as background prevents peaks of CU utilization from triggering [throttling](compute-capacity-smoothing-throttling.md#throttling).

:::image type="content" source="media/usage-reporting/throttling-explore.png" alt-text="A screenshot of the explore button in the Microsoft Fabric Capacity Metrics app." lightbox="media/usage-reporting/throttling-explore.png":::

### Timepoint drill through graph

This table in the Microsoft Fabric Capacity Metrics app provides a detailed view of utilization at specific timepoints. The amount of capacity provided by the given SKU per 30-second period is shown, along with the breakdown of interactive and background operations.

:::image type="content" source="media/usage-reporting/drill-through.png" alt-text="A screenshot of the Timepoint drill through graph in the Microsoft Fabric Capacity Metrics app." lightbox="media/usage-reporting/drill-through.png":::

Top use cases for this view include:

- Identification of a user who scheduled or ran an operation: values can be either "User@domain.com", "System", or "Power BI Service".
    - Examples of user generated statements include running T-SQL queries or activity in the Fabric portal, such as the SQL Query editor or Visual Query editor.
    - Examples of "System" generated statements include metadata synchronous activities and other system background tasks that are run to enable faster query execution.
- Identification of an operation status: values can be either "Success", "InProgress", "Cancelled", "Failure", "Invalid", or "Rejected".
    - The "Cancelled" status are queries cancelled before completing.
    - The "Rejected" status can occur because of resource limitations.
- Identification of an operation that consumed many resources: sort the table by **Total CU(s)** descending to find the most expensive queries, then use **Operation Id** to uniquely identify an operation. This is the distributed statement ID, which can be used in other monitoring tools like dynamic management views (DMVs) for end-to-end traceability, such as in `dist_statement_id` in [sys.dm_exec_requests](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql?view=fabric&preserve-view=true).

### Billing example

Consider the following query:

```sql
SELECT * FROM Nyctaxi;
```

For demonstration purposes, assume the billing metric accumulates 100 CPU seconds.

The cost of this query is **CPU time times the price per CU**. Assume in this example that the price per CU is $0.18/hour. The cost would be (100 x 0.18)/3600 = $0.005.

The numbers used in this example are for demonstration purposes only and not actual billing metrics.

## Considerations

Consider the following usage reporting nuances:

- Cross database reporting: When a T-SQL query joins across multiple warehouses (or across a Warehouse and a SQL Endpoint), usage is reported against the originating resource.
- Queries on system catalog views and dynamic management views are billable queries.
- **Duration(s)** field reported in Fabric Capacity Metrics App is for informational purposes only. It reflects the statement execution duration and might not include the complete end-to-end duration for rendering results back to the web application like the [SQL Query Editor](sql-query-editor.md) or client applications like [SQL Server Management Studio](/sql/ssms/download-sql-server-management-studio-ssms) and [Azure Data Studio](/sql/azure-data-studio/download-azure-data-studio).

## Related content

- [Monitor connections, sessions, and requests using DMVs](monitor-using-dmv.md)
- [Workload management](workload-management.md)
- [Synapse Data Warehouse in Microsoft Fabric performance guidelines](guidelines-warehouse-performance.md)
- [What is the Microsoft Fabric Capacity Metrics app?](../enterprise/metrics-app.md)
- [Smoothing and throttling in Fabric Data Warehousing](compute-capacity-smoothing-throttling.md)
- [Understand your Azure bill on a Fabric capacity](../enterprise/azure-billing.md)
- [Understand the metrics app overview page](../enterprise/metrics-app-overview-page.md)

## Next step

> [!div class="nextstepaction"]
> [How to: Observe Synapse Data Warehouse utilization trends](how-to-observe-utilization.md)