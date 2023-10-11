---
title: What is the admin monitoring workspace?
description: Understand the Microsoft Fabric monitoring workspace and the reports it holds.
author: KesemSharabi
ms.author: kesharab
ms.topic: overview
ms.custom: build-2023
ms.date: 09/26/2023
---

# What is the admin monitoring workspace?

[!INCLUDE [preview-note](../includes/preview-note.md)]

The *Admin monitoring* workspace is designed to provide admins with monitoring capabilities for their organization. Using the admin monitoring workspace resources, admins can perform security and governance tasks such as audits and usage checks.

## Prerequisites

To use the admin monitoring workspace, you need to be an admin with one of these roles.

* Microsoft 365 *Global administrator*

* *Fabric administrator*

## Access the admin monitoring workspace

The admin monitoring workspace is enabled for [Microsoft Fabric admins](microsoft-fabric-admin.md) that have the *Fabric admin* role. Admins can also share its content with other users. Users with viewer permissions that are not admins, can view the admin monitoring workspace by navigating to the workspace URL.

The admin monitoring workspace is automatically installed during the first time any Microsoft Fabric admin accesses it. To access the admin monitoring workspace, follow these steps:

1. Log into Microsoft Fabric with your account.

2. From the left pane, select **Workspaces**.

3. Select **Admin monitoring**. When you select this option for the first time, the required items are automatically installed.

## Reports and datasets

In the monitoring workspace, you can use the [Feature Usage and Adoption](feature-usage-adoption.md) report as is. You can also connect to this report's dataset, and create a solution that's optimized for your organization.

### Manage access

There are several ways you can manage access to content of the admin monitoring workspace. If you're the admin of the workspace, you have a *member* workspace role and you can grant access to any of its items with or without share and build permissions.

* **Workspace** - Learn how to to give users access to the workspace in [manage workspace](../admin/portal-workspaces.md). You can only grant other users a viewer role. Once a viewer role is provided, it can't be taken away.

* **Report** - You can [share a report](/power-bi/connect-data/service-datasets-share) with other users.

* **Dataset** - You can [share access to a dataset](/power-bi/connect-data/service-datasets-share) with other users. Once a dataset is shared, you can't unshare it.

### Refreshes

The admin monitoring workspace is automatically refreshed once a day. The refresh takes place about 10 minutes after the admin workspace was accessed for the first time.

For the refresh to work, the admin that accessed the workspace for the first time, has to:

* Keep his *Global administrator* or *Fabric administrator* role. If the role of the admin who first accessed the workspace changes, the admin monitoring workspace will not be refreshed.

* If the workspace creator uses [Privileged Identity Management (PIM)](/azure/active-directory/privileged-identity-management/pim-configure), it has to be enabled during the scheduled refresh.

## Considerations and limitations

* The admin monitoring workspace is a read-only workspace. [Workspace roles](/power-bi/collaborate-share/service-roles-new-workspaces#workspace-roles) don't have the same capabilities as they do in other workspaces. Users, including admins, are not able to edit or view properties of items such as datasets and reports in the workspace.

* Sovereign clouds are not supported.

* Lineage view of the workspace isn't supported.

## Next steps

* [Admin overview](microsoft-fabric-admin.md)

* [Feature usage and adoption report](feature-usage-adoption.md)
