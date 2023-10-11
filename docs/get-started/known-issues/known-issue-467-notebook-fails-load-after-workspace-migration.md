---
title: Known issue - Notebook fails to load after workspace migration
description: A known issue is posted where a notebook fails to load after workspace migration
author: mihart
ms.author: jessicamo
ms.topic: troubleshooting 
ms.date: 08/03/2023
ms.custom: known-issue-467
---

# Known issue - Notebook fails to load after workspace migration

If you migrate your workspace that contains Reflex or Kusto items to another capacity, may see issues loading a notebook within that workspace.

**Status:** Open

**Product Experience:** Data Engineering

## Symptoms

When you try to open your notebook, you see an error message similar to "Loading Notebook... Failed to get content of notebook.  TypeError: Failed to fetch".

## Solutions and workarounds

To mitigate the issue, you can either:

- Migrate your workspace back to its original capacity
- Or delete the Reflex or Kusto item and then migrate your workspace

## Next steps

- [About known issues](https://support.fabric.microsoft.com/known-issues)
