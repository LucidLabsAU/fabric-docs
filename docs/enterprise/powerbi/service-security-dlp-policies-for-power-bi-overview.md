---
title: Data loss prevention policies for Power BI overview
description: Learn about data loss prevention policies for Power BI.
author: paulinbar
ms.author: painbar
manager: kfollis
ms.service: powerbi
ms.subservice: powerbi-eim
ms.topic: conceptual
ms.custom:
ms.date: 04/20/2023
LocalizationGroup: Data from files
---

# Data loss prevention policies for Power BI

To help organizations detect and protect their sensitive data, Power BI supports [Microsoft Purview Data Loss Prevention (DLP) polices](/microsoft-365/compliance/dlp-learn-about-dlp). When a DLP policy for Power BI detects a sensitive dataset, a policy tip can be attached to the dataset in the Power BI service that explains the nature of the sensitive content, and an alert can be registered in the data loss prevention **Alerts** tab in the Microsoft Purview compliance portal for monitoring and management by administrators. In addition, email alerts can be sent to administrators and specified users.

## Considerations and limitations

* DLP policies for Power BI are defined in the [Microsoft Purview compliance portal](https://go.microsoft.com/fwlink/p/?linkid=2077149).
* DLP policies apply to workspaces. Only workspaces hosted in [Premium capacities](./service-premium-what-is.md) are supported.
* DLP dataset evaluation workloads impact capacity. See [CPU metering for DLP policy evaluation](#cpu-metering-for-dlp-policy-evaluation) for more information.
* DLP policy templates aren't yet supported for Power BI DLP policies. When creating a DLP policy for Power BI, choose the "custom policy" option.
* Power BI DLP policy rules currently support sensitivity labels and sensitive info types as conditions.
* DLP policies for Power BI aren't supported for sample datasets, [streaming datasets](../connect-data/service-real-time-streaming.md), or datasets that connect to their data source via [DirectQuery](../connect-data/desktop-use-directquery.md) or [live connection](../connect-data/desktop-directquery-about.md#live-connections). This includes datasets with mixed storage, where some of the data comes via import-mode and some comes via DirectQuery.
* [Exact data match (EDM) classifiers](/microsoft-365/compliance/sit-learn-about-exact-data-match-based-sits) and [trainable classifiers](/microsoft-365/compliance/classifier-learn-about?view=o365-worldwide)are not supported by DLP for Power BI. If you select an EDM or trainable classifier in the condition of a policy, the policy will yield no results even if the dataset does in fact contain data that satisfies the EDM or trainable classifier. Other classifiers specified in the policy will return results, if any.
* DLP policies for Power BI aren't supported in the China North region. See [How to find the default region for your organization](../admin/service-admin-where-is-my-tenant-located.md#how-to-find-the-default-region-for-your-organization) to learn how to find your organization's default data region.

## Licensing and permissions

### SKU/subscriptions licensing

Before you get started with DLP for Power BI, you should confirm your [Microsoft 365 subscription](https://www.microsoft.com/microsoft-365/compare-microsoft-365-enterprise-plans?rtc=1). The admin account that sets up the DLP rules must be assigned one of the following licenses:

* Microsoft 365 E5
* Microsoft 365 E5 Compliance
* Microsoft 365 E5 Information Protection & Governance

### Permissions

Data from DLP for Power BI can be viewed in [Activity explorer](/microsoft-365/compliance/data-classification-activity-explorer). There are four roles that grant permission to activity explorer; the account you use for accessing the data must be a member of any one of them.

* Global administrator
* Compliance administrator
* Security administrator
* Compliance data administrator

## CPU metering for DLP policy evaluation

DLP policy evaluation uses CPU from the premium capacity associated with the workspace where the dataset being evaluated is located. CPU consumption of the evaluation is calculated as 30% of the CPU consumed by the action that triggered the evaluation. For example, if a refresh action costs 30 milliseconds of CPU, the DLP scan will cost another 9 milliseconds. This fixed 30% additional CPU consumption for DLP evaluation helps you predict the impact of DLP policies on your overall Capacity CPU utilization, and perform capacity planning when rolling out DLP policies in your organization.

Use the Power BI Premium Capacity Metrics App to monitor the CPU usage of your DLP policies. For more information, see [Use the Premium metrics app](./service-premium-metrics-app.md).

>[!NOTE]
>Users with PPU licenses do not incur the DLP policy evaluation costs described above, as these costs are covered for them up front by their PPU license.

## How do DLP policies for Power BI work

You define a DLP policy in the data loss prevention section of the compliance portal. In the policy, you specify the sensitivity labels and/or sensitive info types you want to detect. You also specify the actions that will happen when the policy detects a dataset that contains sensitive data of the kind you specified. DLP policies for Power BI support two actions:

* User notification via policy tips.
* Alerts. Alerts can be sent by email to administrators and users. Additionally, administrators can monitor and manage alerts on the **Alerts** tab in the compliance portal. 

When a dataset is evaluated by DLP policies, if it matches the conditions specified in a DLP policy, the actions specified in the policy occur. A dataset is evaluated against DLP policies whenever one of the following events occurs:

* Publish
* Republish
* On-demand refresh
* Scheduled refresh

>[!NOTE]
> DLP evaluation of the dataset does not occur if either of the following is true:
> * The initiator of the event is a service principal.
> * The dataset owner is either a service principal or a B2B user.

## What happens when a dataset is flagged by a Power BI DLP policy

When a DLP policy detects an issue with a dataset:
* If "user notification" is enabled in the policy, the dataset will be marked in the Power BI service with a shield that indicates that a DLP policy has detected an issue with the dataset.

    :::image type="content" source="./media/service-security-dlp-policies-for-power-bi-overview/power-bi-dlp-policy-tip-on-dataset.png" alt-text="Screenshot of policy tip badge on dataset in lists.":::

    Open the dataset details page to see a policy tip that explains the policy violation and how the detected type of sensitive information should be handled.

    :::image type="content" source="./media/service-security-dlp-policies-for-power-bi-overview/power-bi-dlp-policy-tip-in-dataset-details.png" alt-text="Screenshot of policy tip on dataset details page.":::

    >[!NOTE]
    > If you hide the policy tip, it doesn’t get deleted. It will appear the next time you visit the page.

* If alerts are enabled in the policy, an alert will be recorded on the data loss prevention **Alerts** tab in the compliance portal, and (if configured) an email will be sent to administrators and/or specified users. The following image shows the **Alerts** tab in the data loss prevention section of the compliance portal.

:::image type="content" source="./media/service-security-dlp-policies-for-power-bi-overview/power-bi-dlp-alerts-tab.png" alt-text="Screenshot of Alerts tab in the compliance portal.":::

## Monitor and manage policy alerts

Log into the [Microsoft Purview compliance portal](https://go.microsoft.com/fwlink/p/?linkid=2077149) and navigate to **Data loss prevention > Alerts**.

:::image type="content" source="./media/service-security-dlp-policies-for-power-bi-overview/power-bi-dlp-alerts-tab.png" alt-text="Screenshot of D L P Alerts tab.":::

Select an alert to start drilling down to its details and to see management options.

## Next steps

* [Learn about data loss prevention](/microsoft-365/compliance/dlp-learn-about-dlp)
* [Get started with Data loss prevention policies for Power BI](/microsoft-365/compliance/dlp-powerbi-get-started)
* [Sensitivity labels in Power BI](service-security-sensitivity-label-overview.md)
* [Audit schema for sensitivity labels in Power BI](service-security-sensitivity-label-audit-schema.md)
* [Power BI implementation planning: Data loss prevention for Power BI](/power-bi/guidance/powerbi-implementation-planning-data-loss-prevention)
