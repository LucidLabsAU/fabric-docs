---
title: Scale your Fabric capacity
description: This article walks through how to scale a Microsoft Fabric capacity in Azure.
author: KesemSharabi
ms.author: kesharab
ms.topic: concept-article
ms.custom: build-2023
ms.date: 06/12/2023
---

# Scale your capacity

[!INCLUDE [preview-note](../includes/preview-note.md)]

This article shows how to scale a Microsoft Fabric capacity in Azure. Scaling allows you to increase or decrease the size of your capacity.

## Prerequisites

To scale your capacity you need:

* An [F SKU capacity](buy-subscription.md#azure-skus)

* To be a [capacity admin](../admin/microsoft-fabric-admin.md#capacity-admin-roles)

## Scale a capacity

1. Sign into the [Azure portal](https://portal.azure.com/).

2. Select the **Microsoft Fabric (preview)** service to see your capacities. You can search for *Microsoft Fabric (preview)* in the search menu.

3. Select the capacity you want to scale. The current size for each capacity is listed under *SKU*. When you make your selection, information about that capacity is displayed next to it. This information includes the current capacity scale  under *SKU*.

4. Under **Scale**, select **Change size**.

5. Select a scale and then select **Resize**.

6. Confirm your tier by viewing the overview tab. The current pricing tier is listed.

## Considerations and limitations

Scaling up a capacity that’s smaller than F64, may take up to three hours. During this time, Fabric Free users may see a request to upgrade to a Power BI Pro license when they try to access a Power BI report.

## Next steps

* [Pause and resume your capacity](pause-resume.md)

* [Understand the metrics app overview page](metrics-app-overview-page.md)
