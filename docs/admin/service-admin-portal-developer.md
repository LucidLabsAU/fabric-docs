---
title: Developer admin settings
description: Learn how to configure Power BI developer admin settings.
author: paulinbar
ms.author: painbar
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-admin
ms.custom: tenant-setting
ms.topic: how-to
ms.date: 08/31/2022
LocalizationGroup: Administration
---

# Developer tenant settings

These settings are configured in the tenant settings section of the Admin portal. For information about how to get to and use tenant settings, see [About tenant settings](/power-bi/admin/service-admin-portal-about-tenant-settings).

:::image type="content" source="media/tenant-settings/developer-settings.png" alt-text="Screenshot of Developer settings options.":::

To manage Power BI developer settings, you must be a Global Admin in Office 365, or have been assigned the Fabric administrator role. For more information about the Fabric administrator role, see [Understanding Power BI administration roles](/power-bi/admin/service-admin-role).

>[!NOTE]
>The developer settings in the Admin portal are different from and not related to the [developer mode](/power-bi/developer/visuals/environment-setup#set-up-power-bi-service-for-developing-a-visual) setting for debugging visuals.

## Embed content in apps

Users in the organization can embed Power BI dashboards and reports in Software as a Service (SaaS) applications. Disabling this setting prevents users from being able to use the REST APIs to embed Power BI content within their application. To learn more, see [What is Power BI embedded analytics?](/power-bi/developer/embedded/embedded-analytics-power-bi).

## Allow service principals to use Power BI APIs

Web apps registered in Azure Active Directory (Azure AD) will use an assigned [service principal](/power-bi/developer/embedded/pbi-glossary#service-principal) to access Power BI APIs without a signed in user. To allow an app to use service principal authentication its service principal must be included in an allowed security group.

You can control who can access service principals by creating dedicated security groups and using these groups in any Power BI tenant level-settings. [Learn more](/power-bi/developer/embedded/embed-service-principal).

## Allow service principals to create and use profiles

An app owner with many customers can use service principal profiles as part of a multi-tenancy solution to enable better customer data isolation and establish tighter security boundaries between customers. To learn more, see [Service principal profiles for multitenancy apps](/power-bi/developer/embedded/embed-multi-tenancy).

## Block ResourceKey Authentication

For extra security, you can block the use of resource key based authentication. The Block ResourceKey Authentication setting applies to streaming and PUSH datasets. If disabled, users will not be allowed send data to streaming and PUSH datasets using the API with a resource key.  

This setting applies to the entire organization. You can't apply it only to a select security group.

## Next steps

- [About tenant settings](/power-bi/admin/service-admin-portal-about-tenant-settings)
