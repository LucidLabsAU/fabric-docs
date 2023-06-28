---
title: How to apply sensitivity labels in Power BI
description: Learn how to apply sensitivity labels on your Power BI reports, dashboards, datasets, dataflows, and .pbix files.
author: paulinbar
ms.author: painbar
ms.service: powerbi
ms.subservice: powerbi-eim
ms.custom: video-RE4M5Gj
ms.topic: how-to
ms.date: 06/29/2023
LocalizationGroup: Data from files
---

# How to apply sensitivity labels in Power BI

Sensitivity labels from Microsoft Purview Information Protection on your reports, dashboards, datasets, dataflows, and .pbix files can guard your sensitive content against unauthorized data access and leakage. Labeling your data correctly with sensitivity labels ensures that only authorized people can access your data. This article shows you how to apply sensitivity labels in the Power BI service and in Power BI Desktop.

For more information about sensitivity labels in Power BI, see [Sensitivity labels in Power BI](service-security-sensitivity-label-overview.md).

#### Give us your feedback

The product team would love to get your **[feedback](https://forms.office.com/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbR-PPBJBIRPlBpEYIBVrF5lRUREtUREJJRzJZSzcyM1pZWU9LOUdSVkFKWC4u)** about Power BI's information protection capabilities and its integration with Microsoft Purview Information Protection. Help us meet your information protection needs! Thanks!

## Apply sensitivity labels in the Power BI service

In the Power BI service, you can apply sensitivity labels to reports, dashboards, datasets, and dataflows.

Here are the requirements needed to apply sensitivity labels in the Power BI service:

- You must have a [Power BI Pro or Premium Per User (PPU) license](./service-admin-purchasing-power-bi-pro.md) and edit permissions on the content you wish to label.
- Sensitivity labels must be enabled for your organization. Contact your Power BI admin if you aren't sure about the configuration.
- You must belong to a security group that has permissions to apply sensitivity labels, as described in [Enable sensitivity labels in Power BI](./service-security-enable-data-sensitivity-labels.md).
- All [licensing and other requirements](./service-security-enable-data-sensitivity-labels.md#licensing-and-requirements) must be met.

When data protection is enabled on your tenant, sensitivity labels appear in the sensitivity column in the list view of dashboards, reports, datasets, and dataflows.

:::image type="content" source="media/service-security-apply-data-sensitivity-labels/apply-data-sensitivity-labels-01.png" alt-text="Screenshot of a workspace with the sensitivity column highlighted." lightbox="media/service-security-apply-data-sensitivity-labels/apply-data-sensitivity-labels-01.png" border="false":::

**To apply or change a sensitivity label on a report or dashboard:**

1. Go to **Settings**.
1. In the settings side pane, go to the Sensitivity label section and select the appropriate sensitivity label.
1. Save the settings.

The following image illustrates these steps on a report:

:::image type="content" source="media/service-security-apply-data-sensitivity-labels/downstream-inheritance-user-consent-checkbox.png" alt-text="Screenshot of the sensitivity label dialog. Confidential for finance is selected." lightbox="media/service-security-apply-data-sensitivity-labels/downstream-inheritance-user-consent-checkbox.png" border="false":::

> [!NOTE]
> If the label is greyed out, you might not have the correct [usage rights](service-security-sensitivity-label-change-enforcement.md) to change the label. If you need to change a sensitivity label and can't, either ask the person who applied the label in the first place to modify it, or contact the Microsoft 365/Office security administrator and request the necessary [usage rights](service-security-sensitivity-label-change-enforcement.md) for the label.

**To apply or change a sensitivity label on a dataset or dataflow:**

1. Go to **Settings**.
1. Select the datasets or dataflows tab, whichever is relevant.
1. Expand the sensitivity labels section and choose the appropriate sensitivity label.
1. Apply the settings.

The following two images illustrate these steps on a dataset.

Select **More options (...)** and then **Settings**.

:::image type="content" source="media/service-security-apply-data-sensitivity-labels/apply-data-sensitivity-labels-05.png" alt-text="Screenshot that shows how to open dataset settings." lightbox="media/service-security-apply-data-sensitivity-labels/apply-data-sensitivity-labels-05.png" border="false":::

On the settings datasets tab, open the sensitivity label section, choose the desired sensitivity label, and select **Apply**.

:::image type="content" source="media/service-security-apply-data-sensitivity-labels/apply-data-sensitivity-labels-06.png" alt-text="Screenshot of the expanded sensitivity label settings." lightbox="media/service-security-apply-data-sensitivity-labels/apply-data-sensitivity-labels-06.png" border="false":::

> [!NOTE]
> If the label is grayed out, you might not have the correct [usage rights](service-security-sensitivity-label-change-enforcement.md) to change the label. If you need to change a sensitivity label and can't, either ask the person who applied the label in the first place to modify it, or contact the Microsoft 365/Office security administrator and request the necessary [usage rights](service-security-sensitivity-label-change-enforcement.md) for the label.

## Apply sensitivity labels in Power BI Desktop

To use sensitivity labels in Power BI Desktop:

- You must have a [Power BI Pro or Premium Per User (PPU) license](./service-admin-purchasing-power-bi-pro.md).
- Sensitivity labels must be enabled for your organization. Contact your Power BI admin if you aren't sure about the configuration.
- You must belong to a security group that has permissions to apply sensitivity labels, as described in [Enable sensitivity labels in Power BI](./service-security-enable-data-sensitivity-labels.md).
- All [licensing and other requirements](./service-security-enable-data-sensitivity-labels.md#licensing-and-requirements) must have been met.
- You must be signed in.

Watch a short video on applying sensitivity labels and then try it out yourself.

> [!NOTE]
> This video might use earlier versions of Power BI Desktop or the Power BI service.

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE4M5Gj]

To apply a sensitivity label on the file you're working on, select the sensitivity button in the home tab. In the pop-up menu, choose the desired label.

:::image type="content" source="media/service-security-apply-data-sensitivity-labels/sensitivity-label-menu-desktop.png" alt-text="Screenshot of a portion of the Power BI Desktop menu with the sensitivity label menu expanded." lightbox='media/service-security-apply-data-sensitivity-labels/sensitivity-label-menu-desktop.png" border="false":::

> [!NOTE]
> If the sensitivity button is greyed out, it might indicate that you don't have an appropriate license or that you don't belong to a security group that has permissions to apply sensitivity labels, as described in [Enable sensitivity labels in Power BI](./service-security-enable-data-sensitivity-labels.md).
>
> If a particular label you wish to change is greyed out, you might not have the correct [usage rights](service-security-sensitivity-label-change-enforcement.md) to change that label. If you need to change a sensitivity label and can't, either ask the person who applied the label in the first place to modify it, or contact the Microsoft 365/Office security administrator and request the necessary [usage rights](service-security-sensitivity-label-change-enforcement.md) for the label.

After you apply the label, it's visible in the status bar.

:::image type="content" source="media/service-security-apply-data-sensitivity-labels/sensitivity-label-in-desktop-status-bar.png" alt-text="Screenshot with the sensitivity label highlighted in the Power BI Desktop status bar." lightbox="media/service-security-apply-data-sensitivity-labels/sensitivity-label-in-desktop-status-bar.png" border="false":::

### Sensitivity labels when uploading or downloading .pbix files to/from the service

When you publish a .pbix file to the Power BI service from Desktop, or when you upload a .pbix file to the Power BI service directly via the **OneLake data hub**, the .pbix file's label is applied to both the report and the dataset that are created in the service. If the .pbix file you're publishing or uploading replaces existing assets (that is, the file has the same name as the .pbix file), you see a dialog prompt. At the prompt, choose whether to keep the labels on the assets or have the .pbix file's label overwrite those labels. If the .pbix file is unlabeled, the labels in the service are retained.

When you download a .pbix file from the Power BI service using **Download this file**, if the report and dataset being downloaded both have labels, and those labels are different, the label that's applied to the .pbix file is the more restrictive of the two.

## Remove sensitivity labels

You can remove sensitivity labels in both the service and in Desktop.

### Service

To remove a sensitivity label from a report, dashboard, dataset, or dataflow, follow the [same procedure used for applying labels in the Power BI service](#apply-sensitivity-labels-in-the-power-bi-service), but choose **(None)** when prompted to classify the sensitivity of the data.

### Desktop

To remove a sensitivity label from a .pbix file, reselect the label in the sensitivity drop-down menu.

## Considerations and limitations

For the list of sensitivity label limitations in Power BI, see [Sensitivity labels in Power BI](service-security-sensitivity-label-overview.md#considerations-and-limitations).

## Next steps

This article described how to apply sensitivity labels in Power BI. The following articles provide more details about data protection in Power BI.

- [Overview of sensitivity labels in Power BI](./service-security-sensitivity-label-overview.md)
- [Enable sensitivity labels in Power BI](./service-security-enable-data-sensitivity-labels.md)
- [Using Microsoft Defender for Cloud Apps controls in Power BI](./service-security-using-defender-for-cloud-apps-controls.md)
