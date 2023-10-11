---
title: Create and manage an eventstream in Microsoft Fabric
description: This article describes how to create and manage an eventstream item with Microsoft Fabric event streams feature.
ms.reviewer: spelluru
ms.author: xujiang1
author: xujxu
ms.topic: how-to
ms.custom: build-2023, build-2023-dataai, build-2023-fabric
ms.date: 05/23/2023
ms.search.form: Event streams
---

# Create and manage an eventstream in Microsoft Fabric

The event streams feature in Microsoft Fabric gives you a centralized place in the Fabric platform to capture, transform, and route real-time events to various destinations with a no-code experience. It integrates your eventstreams seamlessly with Azure Event Hubs, KQL databases, and lakehouses.

[!INCLUDE [preview-note](../../includes/preview-note.md)]

## Prerequisites

Before you start, you must complete the following prerequisite:

- Get access to a **premium workspace** with **Contributor** or above permissions.

## Create an eventstream

You can create an eventstream on the **Workspace** page, the **Real-Time Analytics experience Homepage**, or the **Create hub** page. Here are the steps:

1. Change your Fabric experience to **Real-Time Analytics** and select **Eventstream** to create a new eventstream in workspace or homepage or create hub.

   - On the **Real-Time Analytics** homepage, select the **Eventstream** tile:

       :::image type="content" source="./media/create-manage-an-eventstream/eventstream-creation-homepage.png" alt-text="Screenshot showing the Eventstream tile on the homepage.":::

   - On the **Workspace** page, select **New** and then **Eventstream**:

       :::image type="content" source="./media/create-manage-an-eventstream/eventstream-creation-workspace.png" alt-text="Screenshot showing where to find the eventstream option in the New menu on the Workspace page." :::

   - On the **Create hub** page, select the **Eventstream** tile:

       :::image type="content" source="./media/create-manage-an-eventstream/eventstream-creation-create-hub.png" alt-text="Screenshot showing the Eventstream tile on the Create hub page." lightbox="./media/create-manage-an-eventstream/eventstream-creation-create-hub.png" :::

1. Enter a **name** for the new eventstream and select **Create**.

   :::image type="content" source="./media/create-manage-an-eventstream/eventstream-creation-naming.png" alt-text="Screenshot showing where to enter the eventstream name on the New Eventstream screen." :::

1. Creation of the new eventstream in your workspace may take a few seconds. Once it’s done, you're directed to the main editor where you can add sources and destinations to your eventstream. See the [Main editor](#main-editor-for-eventstreams) section for details.

   :::image type="content" source="./media/create-manage-an-eventstream/eventstream-creation-completed.png" alt-text="Screenshot showing the eventstream creation completed." lightbox="./media/create-manage-an-eventstream/eventstream-creation-completed.png" :::

## Manage an eventstream

After you create an eventstream, you can edit and manage the eventstream in your workspace.

- **Delete**: Delete the eventstream from your workspace.
- **Settings**: Change the eventstream name, edit the sensitivity, and set the endorsement to Certified or Promoted Power BI content.
- **Add to Favorites**: Add the eventstream to the **Home** > **Favorites** tab.
- **View lineage**: See an overview of where all the data comes from and goes to.
- **View details**: View detailed information about your eventstream.

    :::image type="content" source="./media/create-manage-an-eventstream/eventstream-management.png" alt-text="Screenshot showing the eventstream management." lightbox="./media/create-manage-an-eventstream/eventstream-management.png" :::

## Main editor for eventstreams

The Microsoft Fabric event streams feature provides a main editor, which is a canvas that allows you to connect to event data sources and destinations with a few clicks. Each tile (node) in the canvas represents a source, a destination, or the eventstream itself. From there, you can preview the event data, monitor the data insights with metrics, and check logs for each of these tiles (nodes).

The following screenshot shows an eventstream with its source and destination configured.

:::image type="content" source="./media/main-editor/eventstream-main-editor.png" alt-text="Screenshot showing an eventstream item overview." lightbox="./media/main-editor/eventstream-main-editor.png" :::

1. **Ribbon**: The ribbon menu provides source and destination options.
2. **Data navigation pane**: This pane allows you to navigate the sources and destinations.
3. **Canvas and diagram view**: This pane provides graphical representation of the entire eventstream topology, from the sources to the destinations. Each source or destination appears as a tile (node) in the canvas.
4. **Configuration and modification pane**: This pane allows you to configure or modify a specific source or destination.
5. **Bottom pane for information, data preview, data insights, and runtime logs**: For each tile (node), the data preview shows you data inside the selected tile (node). This section also summarizes runtime logs where the runtime logs exist in certain sources or destinations. It also provides metrics for you to monitor the data insights for certain sources or destinations, such as input events, output events, incoming messages, outgoing messages, etc.

## Next steps

- [Add and manage eventstream sources](./add-manage-eventstream-sources.md)
- [Add and manage eventstream destinations](./add-manage-eventstream-destinations.md)
