---
title: Understand the metrics app timepoint page
description: Learn how to read the Microsoft Fabric Capacity Metrics app's explore page.
author: KesemSharabi
ms.author: kesharab
ms.topic: how to
ms.custom: build-2023
ms.date: 05/23/2023
---

# Understand the metrics app timepoint page

[!INCLUDE [preview-note](../includes/preview-note.md)]

All the activities in the capacity are ranked according to their compute impact. Use this page to understand which [*interactive* and *background*](/power-bi/enterprise/service-premium-interactive-background-operations) operations contributed the most to CU usage.

>[!NOTE]
>Start and end times may occur before or after the displayed time period, due to [background](/power-bi/enterprise/service-premium-interactive-background-operations#background-operations) [smoothing](/power-bi/enterprise/service-premium-smoothing) operations.

When the total combined CU for *interactive* and *background* operations exceeds the 30 second timepoint allowance, the capacity is overloaded and depending on whether autoscale is enabled or not, throttling is applied.

* **Autoscale is enabled** - If the capacity has autoscale enabled, a new capacity unit (CU) will get added for the next 24 hours and will be shown as an increased value in the *CU Limit* line in the [Capacity utilization and throttling](metrics-app-overview-page.md#capacity-utilization-and-throttling) chart and CU (s) card will changes its color to yellow.

    >[!NOTE]
    >When autoscale is enabled, if the capacity reaches the maximum number of capacity units (CUs) allowed by the autoscale operation, throttling is applied.

* **Autoscale isn't enabled** - If autoscale isn't enabled, throttling gets applied to every interactive operation in the subsequent timepoint.

## Top row visuals

This section describes the operations of the visuals in the top row of the timepoint page.

* **Top left card** - Displays the timepoint used to get to this page.

* **Heartbeat line chart** - Shows a 60 minute window of CU activity. Use this visual to establish the duration of peaks and troughs.

    * *Vertical light green line* - The timepoint you currently viewed. The visual shows the 30 minutes of CU activity leading to the selected timepoint, as well as the 30 minutes of CU activity after the selected timepoint.

    * *CU % Limit* - The capacity allowance.

    * *CU %* - The capacity usage.

    There are also three colors describing the capacity usage:

    * *Green* - The percent of CU consumption.

    * *Red* - The percent of CU consumption limit.

    * *Yellow* - The percent of CU consumption that's autoscaled.

    >[!NOTE]
    >If the yellow line is above the red line the capacity is overloaded.

* **Interactive operations card** - Displays the total number of interactive operations that contributed to the CU's activity during this timepoint.

* **Background operations card** - Displays the total number of background operations that contributed to the CU's activity during this timepoint.

* **SKU card** - Displays the current SKU.

* **Capacity CU card** - Displays the total number of CU seconds allowed for this capacity, for a given 30 second timepoint window. User can hover over card to see bifurcation of Base CU (s) and Autoscale CU (s). When autoscale is enabled, the card will change its color to yellow.

## Interactive Operations

A table showing every [interactive operation](/power-bi/enterprise/service-premium-interactive-background-operations) that contributed CU usage in the viewed timepoint. Once an interactive operation completes, all of the CU seconds used by it get attributed to the timepoint window.

* **Items** - The name of the item, its type, and its workspace details.

* **Operation** - The type of interactive operation.

* **Start** - The time the interactive operation began.

* **End** - The time the interactive operation finished.

* **Status** - An indication showing if the operation succeeded or failed. Canceled operations are reported as failed operations.

    >[!NOTE]
    >CU usage for failed operations is counted when determining if the capacity is in overload.

* **User** - The name of the user that triggered the interactive operation.

* **Duration (s)** - The number of seconds the interactive operation took to complete.

* **Total CU (s)** - The number of CU seconds used by the interactive operation. This metric contributes to determine if the capacity exceeds the total number of CU seconds allowed for the capacity.

* **Timepoint CU (s)** - The number of CU seconds assigned to the interactive operation in the current timepoint.

* **Throttling (s)** - The number of seconds of throttling applied to this interactive operation because of the capacity being overloaded in the previous timepoint.

* **% Of Base Capacity** - Interactive CU operations as a proportion of the base capacity allowance.

* **Billing type** - Displays information if the item is billable or not.

    * **Billable** - Indicates that operations for this item are billable.

    * **Non-Billable**  - Indicates that operations for this item are non-billable.

* **Operation ID** - A unique identifier assigned to an individual operation.

## Background Operations

A table showing every background operation that contributed CU usage to the viewed timepoint. Every background operation that completed in the prior 24 hours (defined as a 2,880 x 30 second timepoint window), contributes a small portion of its total usage to the CU value. This means that a background operation that completed the previous day can contribute some CU activity to determine if the capacity is in overload. For more information see [performance smoothing](/power-bi/enterprise/service-premium-smoothing).

All the columns in the background operations table are similar to the ones in the [interactive operations](#interactive-operations) table. However, the background operations table doesn't have a *users* column.

## Burndown table

A table showing the *add*, *burndown* and *cumulative* percent by experiences, for the last 30 seconds.

* **Experience** - The name of the experience.

* **Add %** - The percentage of carryforward added compared to the capacity, for the last 30 seconds.

* **Burndown %** - The percentage of carryforward burndown compared to the capacity, for the last 30 seconds. 

* **Cumulative %** - The percentage of cumulative carryforward compared to the capacity, for the last 30 seconds.

## Overages 

You can change the overages visual scale to display 10 minutes, 60 minutes and 24 hours. Carryforward only takes into account billable operations.

* **Add %** - The green columns represent the percentage of carryforward added within the specified timepoint window.
  
* **Burndown %** - The blue columns represent the percentage of carryforward burned down within the specified timepoint window.
  
* **Cumulative %** - The red line represents the cumulative carryforward within the specified timepoint window.



## Next steps

[Understand the metrics app overview page?](metrics-app-overview-page.md)