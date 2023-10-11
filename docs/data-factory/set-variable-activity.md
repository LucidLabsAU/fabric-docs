---
title: Set Variable activity
description: Learn how to use the Set Variable activity to add a value to an existing array variable defined in Fabric pipeline.
ms.reviewer: jburchel
ms.author: chez
author: chez-charlie
ms.topic: how-to
ms.date: 08/23/2023
---

# Use the Set Variable activity in Fabric

Use the Set Variable activity to set the value of an existing variable of type String, Bool, or Array defined in a pipeline in Data Factory for Microsoft Fabric or use the Set Variable activity to set a pipeline return value.

[!INCLUDE [df-preview-warning](includes/data-factory-preview-warning.md)]

## Prerequisites

To get started, you must complete the following prerequisites:

- A tenant account with an active subscription. [Create an account for free](../get-started/fabric-trial.md).
- A workspace is created.

## Add a Set Variable activity to a pipeline with UI

To use a Set Variable activity in a pipeline, complete the following steps:

### Creating the activity

1. Create a new pipeline in your workspace.
1. Search for **Set Variable** in the pipeline **Activities** pane, and select it to add it to the pipeline canvas. You may need to expand the list of available activities using the dropdown **+** button at the far right of the toolbar if the window size isn't large enough to display it directly.

   :::image type="content" source="media/set-variable-activity/add-set-variable-activity.png" lightbox="media/set-variable-activity/add-set-variable-activity.png" alt-text="Screenshot of the Fabric UI with the Activities pane and Append variable activity highlighted.":::

1. Select the new activity on the canvas if it isn't already selected.

   :::image type="content" source="media/set-variable-activity/set-variable-general-settings.png" alt-text="Screenshot showing the General settings tab of the Set Variable activity.":::

Refer to the [**General** settings](activity-overview.md#general-settings) guidance to configure the **General** settings tab.

### Set Variable settings

On the **Settings** tab, you can choose either a pipeline variable, or you can specify a return value for the pipeline directly. This example shows a single return value called MyVariable, with a string data type, and value "Some value".

:::image type="content" source="media/set-variable-activity/set-variable-pipeline-return-value.png" alt-text="Screenshot showing the Append variable activity settings tab, highlighting the tab.":::

You can add multiple values for the **Pipeline return value** using the **+ New** button (or the **Delete** button to remove them). Likewise, when setting a **Pipeline variable**, you can choose any previously defined variables from the **Name** dropdown box, or add new one(s) with the **+ New** button. If you want to create pipeline variables independently of the Set Variable activity, select the background in the pipeline canvas (to show the pipeline properties pages), and then use the **Variables** tab in the pipeline settings to create them. Then you can select them from the dropdown list in the Set Variable **Settings** when choosing **Pipeline variable**.

## Save and run or schedule the pipeline

Although Set Variable is typically used with other activities, it can be run directly as is. To run the pipeline here, switch to the **Home** tab at the top of the pipeline editor, and select the save button to save your pipeline.  Select **Run** to run it directly, or **Schedule** to schedule it.  You can also view the run history here or configure other settings.

:::image type="content" source="media/lookup-activity/pipeline-home-tab.png" alt-text="Screenshot showing the Home tab in the pipeline editor with the tab name, Save, Run, and Schedule buttons highlighted.":::

## Next steps

[How to monitor pipeline runs](monitor-pipeline-runs.md)
