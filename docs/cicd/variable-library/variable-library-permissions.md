---
title: The Microsoft Fabric Variable library permissions
description: Understand who can access Variable libraries and their values.
author: mberdugo
ms.author: monaberdugo
ms.reviewer: Lee
ms.service: fabric
ms.subservice: cicd
ms.topic: concept-article
ms.custom:
ms.date: 08/15/2024
ms.search.form: Introduction to Variable libraries, Manage Variable libraries, Variable library permissions, variable types
#customer intent: As a developer, I want to learn how to use the Variable library item and who has permission to view and edit them.
---

# Variable library permissions (preview)

The Microsoft Fabric Variable library permissions are aligned with the Fabric workspace model. This article explains who can access Variable libraries and their values.

## Variable library item permissions

Permissions are given according to your workspace role:

Workspace role | Permissions
---------------|------------
Viewer | Can view the Variable library item.
Contributor | Can view, add, edit, and delete the Variable library item.
Member | Can view, add, edit, and delete the Variable library item.
Admin | Can view, add, edit, and delete the Variable library item.

To set an item as a variable value in a Variable library , you need to have at least read permission for that item. For example, if you want to set the value of a variable to be a lakehouse, you need to have read permission for the lakehouse.

For more information about workspace roles, see [Roles in workspaces in Microsoft Fabric](../../get-started/roles-workspaces.md).

## Variable permissions

There's no permission management in an item level or a variable level. Permission for each variable is the same as the permissions for the entire item.
