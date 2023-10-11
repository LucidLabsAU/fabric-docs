---
title: Git integration admin settings
description: Learn about what the feature switches affecting git integration do and how to use them.
author: mberdugo
ms.author: monaberdugo
ms.topic: how-to
ms.custom: build-2023
ms.date: 09/08/2023
---

# Git integration tenant settings

[!INCLUDE [preview-note](../includes/preview-note.md)]

The git integration tenant admin settings are configured in the tenant settings section of the Admin portal. For information about how to get to and use tenant settings, see [About tenant settings](/power-bi/admin/service-admin-portal-about-tenant-settings).

> [!IMPORTANT]
> The switches that control git integration are part of Microsoft Fabric and only work if the [Fabric admin switch](./fabric-switch.md) is turned on. If Fabric is disabled, git integration can't work regardless of the status of these switches.

## Users can synchronize workspace items with their Git repositories (Preview)

Users can synchronize a workspace with a git repository, edit their workspace, and update their git repos using the git integration tool. You can enable git integration for the entire organization, or for a specific group. Turn off this setting to prevent users from syncing workspace items with their Git repositories.

To learn more, see [Introduction to Git integration](../cicd/git-integration/intro-to-git-integration.md).

To get started with Git integration, see [Manage a workspace with Git](../cicd/git-integration/git-get-started.md).

## Users can export items to Git repositories in other geographical locations (Preview)

If a workspace capacity is in one geographic location (for example, Central US) while the Azure DevOps repo is in another location (for example, West Europe), the Fabric admin can decide whether to allow users to commit metadata (or perform other git actions) to another geographical location. Only the metadata of the item is exported. Item data and user related information are not exported.  
Enable this setting to allow all users, or a specific group or users, to export metadata to other geographical locations.

## Users can export workspace items with applied sensitivity labels to Git repositories (Preview)

Sensitivity labels aren't included when exporting an item. Therefore, the Fabric admin can choose whether to block the export of items that have sensitivity labels, or to allow it even though the sensitivity label won't be included.

Enable this setting to allow all users, or a specific group of users, to export items without their sensitivity labels.

Learn more about [sensitivity labels](../get-started/apply-sensitivity-labels.md).

## Next steps

- [About tenant settings](/power-bi/admin/service-admin-portal-about-tenant-settings)
