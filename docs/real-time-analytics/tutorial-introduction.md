---
title: Real-Time Analytics Tutorial- Introduction
description: Get started with Synapse Real-Time Analytics in Microsoft Fabric.
ms.reviewer: tzgitlin
ms.author: yaschust
author: YaelSchuster
ms.topic: tutorial
ms.custom: build-2023
ms.date: 09/28/2023
ms.search.form: Get started
---

# Real-Time Analytics Tutorial- Introduction

[!INCLUDE [preview-note](../includes/preview-note.md)]

Real-Time Analytics in Microsoft Fabric is a fully managed big data analytics platform optimized for streaming and time-series data. It utilizes a query language and engine with exceptional performance for searching structured, semi-structured, and unstructured data with high performance. Real-Time Analytics is fully integrated with the entire suite of Fabric products, for both data loading and advanced visualization scenarios. For more information, see [What is Real-Time Analytics in Fabric?](overview.md).

## Scenario

This tutorial is based on sample streaming data called *New York Yellow Taxi trip data*. The dataset contains trip records of New York's yellow taxis, with fields capturing pick-up and drop-off dates/times, pick-up and drop-off locations, trip distances, itemized fares, rate types, payment types, and driver-reported passenger counts. This data doesn't contain latitude and longitude data, which will be loaded from a blob container and joined together with the streaming data in a later step.

You'll use the streaming and query capabilities of Real-Time Analytics to answer key questions about the trip statistics, taxi demand in the boroughs of New York and related insights, and build Power BI reports.

Specifically, in this tutorial, you learn how to:

> [!div class="checklist"]
>
> * Create a KQL database
> * Enable data copy to OneLake
> * Create an eventstream
> * Stream data from Eventstream to your KQL database
> * Get additional historical data
> * Explore data with KQL and SQL
> * Create a KQL queryset
> * Use advanced KQL queries
> * Create a Power BI report
> * Clean up resources

## Prerequisites

To successfully complete this tutorial, you need a [workspace](../get-started/create-workspaces.md) with a Microsoft Fabric-enabled [capacity](../enterprise/licenses.md#capacity).

## Next steps

> [!div class="nextstepaction"]
> [Tutorial part 1: Set up resources](tutorial-1-resources.md)
