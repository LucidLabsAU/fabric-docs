---
title: Create an eventstream in Microsoft Fabric
description: This article describes how to create an eventstream item with Microsoft Fabric event streams feature.
ms.reviewer: spelluru
ms.author: xujiang1
author: xujxu
ms.topic: how-to
ms.custom:
  - ignite-2024
ms.date: 11/18/2024
ms.search.form: Eventstreams Overview
zone_pivot_group_filename: real-time-intelligence/event-streams/zone-pivot-groups.json
zone_pivot_groups: event-streams-standard-enhanced
---

# Create an eventstream in Microsoft Fabric
This article describes how to create a Fabric eventstream. The enhanced capabilities are enabled by default now, so use the content in the **Enhanced Capabilities** tab to create an eventstream.

If you have eventstreams that were created using standard capabilities, those eventstreams will continue to work. You can still edit and publish them as usual. We recommend that you create a new eventstream to replace standard eventstreams so that you can take advantage of additional capabilities and benefits of enhanced eventstreams.

::: zone pivot="enhanced-capabilities"  

## Prerequisites
Before you start, you must complete the following prerequisite:

- Get access to a workspace in the Fabric capacity license mode (or) the Trial license mode with Contributor or higher permissions.


## Create an eventstream

[!INCLUDE [create-an-eventstream](./includes/create-an-eventstream.md)]

## Next step
- [Add sources to the eventstream](./add-manage-eventstream-sources.md)
- [Add destinations to the eventstream](./add-manage-eventstream-destinations.md)

::: zone-end

::: zone pivot="standard-capabilities"

The eventstreams feature in Microsoft Fabric gives you a centralized place in the Fabric platform to capture, transform, and route real-time events to various destinations with a no-code experience. It integrates your eventstreams seamlessly with Azure Event Hubs, KQL databases, and lakehouses.

> [!IMPORTANT]
> Use this tab if you are using Fabric event streams without enhanced capabilities. If you are using enhanced capabilities, use the **Enhanced Capabilities** tab. 


## Prerequisites

Before you start, you must complete the following prerequisite:

- Get access to a workspace in the Fabric capacity license mode (or) the Trial license mode with Contributor or higher permissions.

## Create an eventstream

You can create an eventstream on the **Workspace** page, the **Real-Time Intelligence experience Homepage**, or the **Create hub** page. Here are the steps:

1. Change your Fabric experience to **Real-Time Intelligence** and select **Eventstream** to create a new eventstream in workspace or homepage or create hub.

   - On the **Real-Time Intelligence** homepage, select the **Eventstream** tile:

       :::image type="content" source="./media/create-manage-an-eventstream/eventstream-creation-homepage.png" alt-text="Screenshot showing the Eventstream tile on the homepage.":::

   - On the **Workspace** page, select **New** and then **Eventstream**:

       :::image type="content" source="./media/create-manage-an-eventstream/eventstream-creation-workspace.png" alt-text="Screenshot showing where to find the eventstream option in the New menu on the Workspace page." :::

   - On the **Create hub** page, select the **Eventstream** tile:

       :::image type="content" source="./media/create-manage-an-eventstream/eventstream-creation-create-hub.png" alt-text="Screenshot showing the Eventstream tile on the Create hub page." lightbox="./media/create-manage-an-eventstream/eventstream-creation-create-hub.png" :::

1. Enter a **name** for the new eventstream and select **Create**.

   :::image type="content" source="./media/create-manage-an-eventstream/eventstream-creation-naming.png" alt-text="Screenshot showing where to enter the eventstream name on the New Eventstream screen." :::

1. Creation of the new eventstream in your workspace can take a few seconds. After the eventstream is created, you're directed to the main editor where you can add sources and destinations to your eventstream. See the [Main editor](#main-editor-for-eventstreams) section for details.

   :::image type="content" source="./media/create-manage-an-eventstream/eventstream-creation-completed.png" alt-text="Screenshot showing the eventstream creation completed." lightbox="./media/create-manage-an-eventstream/eventstream-creation-completed.png" :::

## Main editor for eventstreams

The Microsoft Fabric event streams feature provides a main editor, which is a canvas that allows you to connect to event data sources and destinations with a few clicks. Each tile (node) in the canvas represents a source, a destination, or the eventstream itself. From there, you can preview the event data, monitor the data insights with metrics, and check logs for each of these tiles (nodes).

The following screenshot shows an eventstream with its source and destination configured.

:::image type="content" source="./media/main-editor/eventstream-main-editor.png" alt-text="Screenshot showing an eventstream item overview." lightbox="./media/main-editor/eventstream-main-editor.png" :::

1. **Ribbon**: The ribbon menu provides source and destination options, complemented by **Activate all** and **Deactivate all** buttons.
2. **Data navigation pane**: This pane allows you to navigate the sources and destinations.
3. **Canvas and diagram view**: This pane provides graphical representation of the entire eventstream topology, from the sources to the destinations. Each source or destination appears as a tile (node) in the canvas.
4. **Configuration and modification pane**: This pane allows you to configure or modify a specific source or destination.
5. **Bottom pane for information, data preview, data insights, and runtime logs**: For each tile (node), the data preview shows you data inside the selected tile (node). This section also summarizes runtime logs where the runtime logs exist in certain sources or destinations. It also provides metrics for you to monitor the data insights for certain sources or destinations, such as input events, output events, incoming messages, outgoing messages, etc.

## Related content

- To learn how to configure an eventstream and more, see [Manage an eventstream](manage-eventstream.md).
- [Add and manage eventstream sources](./add-manage-eventstream-sources.md)
- [Add and manage eventstream destinations](./add-manage-eventstream-destinations.md)

::: zone-end
