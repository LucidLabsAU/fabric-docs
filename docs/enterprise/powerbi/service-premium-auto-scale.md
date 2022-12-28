---
title: Using Autoscale with Power BI Premium
description: Learn how to configure an Azure subscription to use with Autoscale and then enable Autoscale in the Power BI Admin portal.
author: KesemSharabi
ms.author: kesharab
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-premium
ms.topic: conceptual
ms.date: 12/27/2022
ms.custom: licensing support
LocalizationGroup: Premium
---

# Using Autoscale with Power BI Premium

Power BI Premium offers scale and performance for Power BI content in your organization. Power BI Premium Gen2 offers improvements such as enhanced performance, greater scale, improved metrics. In addition, Premium Gen2 enables customers to automatically add compute capacity to avoid slowdowns under heavy use, using **Autoscale**.

:::image type="content" source="media/service-premium-auto-scale/pbi-auto-scale-on.png" alt-text="Screenshot of the Power BI Admin portal screen showing P1 capacity settings.":::

Autoscale uses an Azure subscription to automatically use more v-cores (virtual CPU cores) when the computing load on your Power BI Premium subscription would otherwise be slowed by its capacity. This article describes the steps necessary to get Autoscale working for your Power BI Premium subscription. Autoscale only works with Power BI Premium Gen2.

To enable Autoscale, the following steps need to be completed:

1. [Configure an Azure subscription to use with Autoscale](#configure-an-azure-subscription-to-use-with-autoscale).

1. [Enable Autoscale in the Power BI Admin portal](#enable-autoscale-in-the-power-bi-admin-portal)

The following sections describe the steps in detail.

>[!NOTE]
>
>* Autoscale isn’t available for Microsoft 365 Government Community Cloud (GCC), due to the use of the commercial Azure cloud.
>* [Embedded Gen 2](../developer/embedded/embedded-analytics-power-bi.md) doesn't provide an out-of-the-box vertical Autoscale feature. To learn about alternative Autoscale options for Embedded Gen2, see [Autoscaling in Embedded Gen2](../developer/embedded/azure-pbie-scale-capacity.md#autoscale-your-capacity).

## Configure an Azure subscription to use with Autoscale

To select and configure an Azure subscription to work with Autoscale, you need to have *contributor* rights for the selected Azure subscription. Any user with *Account admin* rights for the Azure subscription can add a user as a *contributor*. In addition, you must be an admin for the Power BI tenant to enable Autoscale.

To select an Azure subscription to work with Autoscale, take the following steps:

1. Sign on to the Azure portal and in the search box type and select **Subscriptions**.

   :::image type="content" source="media/service-premium-auto-scale/azure-auto-scale-search.png" alt-text="Screenshot of the Azure portal showing the word subscriptions in the search box." lightbox="media/service-premium-auto-scale/azure-auto-scale-search.png":::

1. From the **Subscriptions** page, select the subscription you want to work with Autoscale.

   :::image type="content" source="media/service-premium-auto-scale/azure-auto-scale-subscriptions.png" alt-text="Screenshot of the Azure portal showing a subscription name highlighted." lightbox="media/service-premium-auto-scale/azure-auto-scale-subscriptions.png":::

1. From the *Settings* selections for your selected subscription, select **Resource groups**.

    :::image type="content" source="media/service-premium-auto-scale/azure-auto-scale-resource-group-option.png" alt-text="Screenshot of the Azure portal showing the subscription pane. Resource groups is highlighted in the settings section." lightbox="media/service-premium-auto-scale/azure-auto-scale-resource-group-option.png":::

1. Select **Create** to create a resource group to use with Autoscale.

    :::image type="content" source="media/service-premium-auto-scale/azure-auto-scale-create-resource-group.png" alt-text="Screenshot of the Azure portal showing the resource group pane. Create is highlighted." lightbox="media/service-premium-auto-scale/azure-auto-scale-create-resource-group.png":::

1. Name your resource group and select **Review + create**. The following image shows an example resource group named *powerBIPremiumAutoscaleCores*. You can name your resource group whatever you want. Make a note of the name of the subscription, and the name of your resource group. You'll need to select it from a list when you configure Autoscale in the Power BI Admin portal.

    :::image type="content" source="media/service-premium-auto-scale/azure-auto-scale-name-resource-group.png" alt-text="Screenshot of the create a resource group page. The resource group text field and the review plus create button are highlighted." lightbox="media/service-premium-auto-scale/azure-auto-scale-name-resource-group.png":::

1. Azure validates the information. After the validation process completes successfully, select **Create**. You receive a notification in the upper-right corner of the Azure portal when the action completes.

    :::image type="content" source="media/service-premium-auto-scale/azure-auto-scale-validation-resource-group.png" alt-text="Screenshot of the create a resource group page after it passes the Azure validation test. The create button is highlighted." lightbox="media/service-premium-auto-scale/azure-auto-scale-validation-resource-group.png":::

## Enable Autoscale in the Power BI Admin portal

After you've selected the Azure subscription to use with Autoscale, and created a resource group as described in the previous section, you're ready to enable Autoscale and associate it with the resource group you created. The person configuring **Autoscale** must be at least a *contributor* for the Azure subscription to successfully complete these steps. You can learn more about [assigning a user to a contributor role for an Azure subscription](/azure/cost-management-billing/manage/add-change-subscription-administrator).

>[!NOTE]
>After creating the subscription and enabling Autoscale in the admin portal, a `Microsoft.PowerBIDedicated/autoScaleVCores` resource is created. Make sure that you don't have any Azure policies that prevent Power BI Premium from provisioning, updating or deleting the `Microsoft.PowerBIDedicated/autoScaleVCores` resource.

The following steps show you how to enable and associate Autoscale with the resource group.

1. Open the **Power BI Admin portal** and select **Capacity settings** from the left pane. Information about your Power BI Premium capacity appears.

    :::image type="content" source="media/service-premium-auto-scale/pbi-auto-scale-off-p2.png" alt-text="Screenshot of the Power BI Admin portal showing capacity settings. Autoscale off and the manage Autoscale button are highlighted.":::

1. Autoscale only works with Power BI Premium Gen2. To enable Gen2 is easy: just move the slider to **Enabled** in the **Premium Generation 2** box.

    :::image type="content" source="media/service-premium-auto-scale/enable-gen2.gif" alt-text="Animation that shows how to enable Premium Generation Two.":::

1. Select **Manage auto-scale**  to enable and configure **Autoscale**. The **Auto-scale settings** pane appears. Select  **Enable auto scale**.

    :::image type="content" source="media/service-premium-auto-scale/pbi-auto-scale-settings-p2.png" alt-text="Screenshot of selecting the Autoscale settings page. The enable Autoscale check box is highlighted.":::

1. Select the Azure subscription to use with Autoscale. Only subscriptions available to the current user are displayed, which is why you must be at least a *contributor* for the subscription. Once your subscription is selected, choose the **Resource group** you created in the previous section, from the list of resource groups available to the subscription. Assign the maximum number of v-cores to use for Autoscale, and then select **Save**.

    :::image type="content" source="media/service-premium-auto-scale/pbi-auto-scale-settings-p2-02.png" alt-text="Screenshot of the Autoscale settings page showing subscription, resource group and Autoscale max settings..":::

1. Power BI applies your changes, then closes the pane and returns the view to **Capacity settings** with the settings you applied. The following image shows the maximum v-cores configured for Autoscale.

    :::image type="content" source="media/service-premium-auto-scale/pbi-auto-scale-on-p2.png" alt-text="Screenshot of the capacity settings screen after Autoscale is set to on and configured.":::

The following short video shows how quickly you can configure Autoscale for Power BI Premium Gen2:

:::image type="content" source="media/service-premium-auto-scale/configure-autoscale.gif" alt-text="Animation that shows how to configure Autoscale for Premium Generation 2.":::

## Next steps

> [!div class="nextstepaction"]
> [What is Power BI Premium Gen2?](service-premium-gen2-what-is.md)

> [!div class="nextstepaction"]
> [Power BI Premium Gen2 FAQ](service-premium-gen2-faq.yml)

> [!div class="nextstepaction"]
> [Power BI Premium Per User FAQ](service-premium-per-user-faq.yml)

> [!div class="nextstepaction"]
> [Add or change Azure subscription administrators](/azure/cost-management-billing/manage/add-change-subscription-administrator)
