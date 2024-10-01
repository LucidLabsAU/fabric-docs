---
title: Data Activator limitations
description: Learn about the limitations of using Data Activator in your applications and dashboards. Data Activator provides real-time insights and analytics for your data.
author: mihart
ms.author: mihart
ms.topic: concept-article
ms.custom: FY25Q1-Linter
ms.search.form: product-reflex
ms.date: 09/09/2024
#customer intent: As a Fabric user I want to learn about Data Activator limitations.
---

# Data Activator limitations

Data Activator is subject to the following general and specific limitations. Before you began your work with Data Activator, review and consider these limitations.

> [!IMPORTANT]
> Data Activator is currently in preview.

## General limitations

* Creating alerts for a report using Dynamic M parameters isn't supported.
* Creating alerts from the Fabric or Power BI Capacity Metrics app isn't supported.

## Supported Power BI visuals

Data activator supports the following Power BI visual types:

* Stacked column
* Clustered column
* Stacked bar
* 100% stacked column
* 100% stacked bar
* Clustered bar
* Ribbon chart
* Line
* Area
* Stacked area
* Line and stacked column
* Line and clustered column
* Pie
* Donut
* Gauge
* Card
* KPI

Data Activator also supports the following map visuals. Data Activator only supports map visuals that use the *Location* field to specify the location of objects on the map. Data Activator doesn't support visuals that use *Latitude* and *Longitude* fields.

* Bing Map
* Filled Map
* Azure Map
* ArcGIS map

## Supported Real-Time Dashboard tiles

Data Activator supports the following tile types in Real-Time Dashboards:

* Time chart
* Bar chart
* Column chart
* Area chart
* Line chart
* Stat
* Multi stat
* Pie Chart

Additionally, for Data Activator to support a tile:

* The data in the tile must not be static.
* The data in the tile must be based on a KQL query.
* The tile must have at most one time range.
* The tile must be filtered by a predefined time range. Using a custom time range isn't supported.
* The tile must not contain time series data (for example, data created using the *make-series* KQL operator)

For more information, see [Limitations on charts with a time axis](data-activator-get-data-real-time-dashboard.md#limitations-on-charts-with-a-time-axis).

## Allowed recipients of email notifications

Each recipient of an email notification must have an internal email address. The recipient must belong to the organization that owns the Fabric tenant. Data Activator doesn't allow email notifications to be sent to either external email addresses or guest email addresses. In addition, the email domain of any email notification recipient must match the email domain of the notification owner.

## Maximum data throughput for eventstream data

For eventstream data sources, Data Activator supports throughput up to 10 events per second. If you send eventstream data to Data Activator at a more frequent rate, Data Activator may throttle the input. When throttled, Data Activator doesn't process all events in the stream. At General Availability (GA), reflex item sources will support thousands of events per second. If you have questions or are interested in early access to updates, post in our [Community Forum](https://community.fabric.microsoft.com/t5/Reflex/bd-p/da_reflex).  

## Maximum data for rule processing limits

Data Activator has a limit on the number of events that are processed in a rule based on the type of data being used in the rule. If your rule exceeds the maximum, Data Activator stops your rule. For event streams, the maximum is 1,000 events per second.

## Maximum number of trigger actions

Data Activator imposes the following limits on the number of actions that may occur in a given time period. If an action exceeds the limit, Data Activator may throttle or cancel the action.

|Trigger action  |Scope  |Limit  |
|---------|---------|---------|
|Email     |Messages/reflex item/hour         |500        |
|Email     |Messages/trigger/recipient/hour   |30         |
|Teams     |Messages/reflex item/hour         |500        |
|Teams     |Messages/trigger/recipient/hour   |30         |
|Teams     |Messages/recipient/hour           |100        |
|Teams     |Messages/Teams tenant/second      |50         |
|PA        |Flow executions/trigger/hour      |10000      |

## Related content

* [Get started with Data Activator](data-activator-get-started.md)
* [Detection conditions in Data Activator](data-activator-detection-conditions.md)
* [Data Activator tutorial using sample data](data-activator-tutorial.md)
* [What is Microsoft Fabric?](../get-started/microsoft-fabric-overview.md)
