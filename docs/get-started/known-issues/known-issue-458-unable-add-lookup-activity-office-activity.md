---
title: Known issue - not able to add Lookup activity output to body object of Office 365.
description: A known issue is posted where a user isn't able to add Lookup activity output to the body object of Office 365.
author: mihart
ms.author: anirmale
ms.topic: troubleshooting 
ms.date: 07/26/2023
ms.custom: known-issue-458
---

# Known issue - not able to add Lookup activity output to body object of Office 365

Currently there's a bug when the user tries to add the output of a Lookup activity as a dynamic content to the body object of Office 365. Office 365 activity hangs indefinitely.

**Status:** Open

**Product Experience:** Data Factory

## Symptoms

Office 365 activity hangs indefinitely when output of Lookup activity is added as a dynamic content to the body object of Office 365

## Solutions and workarounds

Wrap the output of the lookup activity in a string, for example @string(activity('Lookup 1').output.firstRow).

## Next steps

- [About known issues](https://support.fabric.microsoft.com/known-issues)
