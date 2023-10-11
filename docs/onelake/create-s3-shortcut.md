---
title: Create an Amazon S3 shortcut
description: Learn how to create an Amazon S3 shortcut.
ms.reviewer: eloldag
ms.author: trolson
author: TrevorLOlson
ms.search.form: Shortcuts
ms.topic: how-to
ms.custom: build-2023
ms.date: 07/16/2023
---

# Create an Amazon S3 shortcut

In this article, you learn how to create an Amazon S3 shortcut inside a Fabric lakehouse. For an overview of shortcuts, see [OneLake shortcuts](onelake-shortcuts.md).

[!INCLUDE [preview-note](../includes/preview-note.md)]

## Prerequisites

- If you don't have a lakehouse, create one by following these steps: [Creating a lakehouse with OneLake](create-lakehouse-onelake.md).

- The IAM user must have the following permissions on the bucket that the shortcut is pointing to.

  - `S3:GetObject`
  - `S3:GetBucketLocation`
  - `S3:ListBucket`

## Create a shortcut

1. Open a lakehouse.

1. Right-click on a directory within the **Lake view** of the lakehouse.

1. Select **New shortcut**.

   :::image type="content" source="media\create-onelake-shortcut\new-shortcut-lake-view.png" alt-text="Screenshot of right click context menu showing where to select New shortcut from the Lake view.":::

[!INCLUDE [amazon-s3-shortcut](../includes/amazon-s3-shortcut.md)]

The lakehouse automatically refreshes. The shortcut appears under **Files** in the **Explorer** pane.

   :::image type="content" source="media\create-onelake-shortcut\folder-shortcut-symbol.png" alt-text="Screenshot showing a Lake view list of folders that display the shortcut symbol.":::

## Next steps

- [Create a OneLake shortcut](create-onelake-shortcut.md)
- [Create an Azure Data Lake Storage Gen2 shortcut](create-adls-shortcut.md)
