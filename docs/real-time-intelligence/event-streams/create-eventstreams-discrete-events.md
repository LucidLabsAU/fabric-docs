---
title: Create eventstreams for discrete events
description: Learn how to create Fabric event streams for discrete events.
ms.reviewer: spelluru
ms.author: xujiang1
author: xujxu
ms.topic: how-to
ms.custom:
  - ignite-2024
ms.date: 11/18/2024
ms.search.form: Source and Destination
---

# Create eventstreams for discrete events (preview)

This article shows you how to create Microsoft Fabric event streams for discrete events.

When you develop applications for real-time analytics, you commonly encounter two types of events: discrete events and continuous events or streams. Microsoft Fabric event streams can ingest and process both discrete and continuous events.



## Understand discrete and continuous events

To build an efficient and scalable eventstream in Fabric, it's important to understand the distinction between discrete events and continuous events or streams.

- **Discrete events**, often referred to as notification events, are individual occurrences that happen at specific points in time. Each event is independent of others and has a clear start and end point. Examples of discrete events include users placing orders on a website or making changes to a database.

- **Continuous events** or **streams** represent a continuous flow or stream of data over time. Unlike discrete events, continuous events don't have distinct start or end points. Instead, they represent a steady and ongoing stream of data, often with no predefined boundaries. Examples include sensor data from IoT devices, stock market ticker data, or social media posts in a real-time feed.

>[!NOTE]
>It's recommended to have either discrete event sources or continuous event (stream) sources, not a mix of both, in one eventstream.

## Supported discrete events

Fabric event streams enable you to build event-driven solutions for capturing system state changes or events in your Fabric data source. Fabric event streams support the following types of discrete events:

|Discrete events|Description|
|----|---------|
|[Azure Blob Storage events](add-source-azure-blob-storage.md)|Generated upon any change made to Azure Blob Storage, such as creation, modification, or deletion of records or files.|
|[Fabric Workspace Item events](add-source-fabric-workspace.md)|Generated upon any change made to a Fabric workspace, including creation, update, or deletion of items.|

## Connect discrete events to eventstreams

In Fabric event streams, you can add a discrete event source into an eventstream and route those events to Real-Time hub. Then you can either transform these events in Fabric event streams or subscribe to them in Real-Time hub. In Real-Time hub, further actions include using Fabric [!INCLUDE [fabric-activator](../includes/fabric-activator.md)] or creating alerts that execute Fabric job items, like Pipeline and Notebook.

### Prerequisite

- Access to a workspace in the Fabric capacity license mode (or) the Trial license mode with Contributor or higher permissions. 
- A Fabric workspace for connecting to Fabric Workspace Item events, or access to an Azure Blob Storage account for connecting to Azure Blob Storage events.


### Create an eventstream
[!INCLUDE [create-an-eventstream](./includes/create-an-eventstream.md)]

### Connect discrete events

To connect discrete events to an eventstream, take the following steps:

1. On the next screen, select **Use external source**.

   :::image type="content" border="true" source="media/external-sources/add-external-source.png" alt-text="A screenshot of selecting Use external source.":::
1. On the **Select a data source** page, select **View all sources**. 

   :::image type="content" border="true" source="media/external-sources/view-all-sources.png" alt-text="A screenshot of selecting View all sources on the Select a data source window.":::
1. On the **Select a data source** screen, select the type of discrete events you want to add to your eventstream, either **Azure Blob Storage events** or **Fabric Workspace Item events**.

   :::image type="content" border="true" source="media/create-eventstreams-discrete-events/select-external-events.png" alt-text="A screenshot of selecting Azure Blob Storage Events.":::
1. Add the event source and publish the eventstream by following the instructions in one of the following articles:

   - For Azure Blob Storage events, see [Add Azure Blob Storage events](add-source-azure-blob-storage.md).
   - For Fabric Workspace Item events, see [Add Fabric workspace item events](add-source-fabric-workspace.md).

Once completed, the eventstream starts capturing discrete events as they occur. In **Real-Time hub**, you can find the events under **Fabric events** or **Azure events**. In the right pane, you can set alerts to take further action. For more information, see the following articles in Real-Time hub documentation:

- [Set alerts on Azure Blob Storage events in Real-Time hub](../../real-time-hub/set-alerts-azure-blob-storage-events.md)
- [Set alerts on Fabric workspace item events in Real-Time hub](../../real-time-hub/set-alerts-fabric-workspace-item-events.md)

[!INCLUDE [known-issues-discrete-events](./includes/known-issues-discrete-events.md)]

## Related content

- [Azure Blob Storage events](add-source-azure-blob-storage.md)
- [Add Fabric workspace item events to an eventstream](add-source-fabric-workspace.md)
