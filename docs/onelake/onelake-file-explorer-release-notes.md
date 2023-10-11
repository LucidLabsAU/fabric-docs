---
title: OneLake File Explorer Release Notes
description: Information about each release of the OneLake file explorer client app for Windows.
ms.reviewer: eloldag
ms.author: eloldag
author: eloldag
ms.topic: how-to
ms.custom: build-2023
ms.date: 07/20/2023
---

# What's new in the latest OneLake file explorer?

Continue reading for information on major updates to OneLake file explorer.

[!INCLUDE [preview-note](../includes/preview-note.md)]

## September 2023 Update (v 1.0.10.0)

### Option to open workspaces and items on the web portal

Now you can seamlessly transition between using OneLake file explorer and the Fabric web portal. When browsing your OneLake data using OneLake file explorer, right click on a workspace and select **OneLake** > **View Workspace Online**.  This opens the workspace browser on the Fabric web portal.  
In addition, you can right click on an item, subfolder or file and select **OneLake** > **View Item Online**.  This opens the item browser on the Fabric web portal.  If you select a subfolder or file, the Fabric web portal always opens the root folder of the item.

### Menu option to open logs directory

With this menu option, you can now easily find your client-side logs, which you may need to troubleshoot issues. Right-click on the OneLake icon in the Windows notification area, located at the far right of the taskbar, and select Select **Diagnostic Operations** > **Open logs directory**. This opens your logs directory in a new Windows file explorer window.

## July 2023 Update (v 1.0.9.0)

### Option to sign in to different accounts

When you install OneLake file explorer, you can now choose which account to sign-in with.  To switch accounts, right click the OneLake icon in the Windows notification area, select “Account” and then “Sign Out”.  Signing out exits OneLake file explorer and pauses the sync.  To sign in with another account, start OneLake file explorer again by searching for "OneLake" using Windows search (Windows + S) and select the OneLake application.  Previously, when you started OneLake file explorer, it automatically used the Microsoft Azure Active Directory identity currently logged into Windows to sync Fabric workspaces and items.  

When you sign in with another account, you see the list of workspaces and items refresh in OneLake file explorer.  If you continue to workspaces associated with the previous account, you can manually refresh the view by clicking “Sync from OneLake”.  Those workspaces are inaccessible while you're signed into a different account.

### Fix known issue during folder moves from outside of OneLake to OneLake

Now when you move a folder (cut and paste or drag and drop) from a location outside of OneLake to OneLake, the contents sync to OneLake successfully.  Previously, you had to trigger a sync by either opening the files and saving them or moving them back out of OneLake and then copying and pasting (versus moving).

## Support lifecycle

Only the most recent version of OneLake file explorer is supported.  Customers who contact support for OneLake file explorer will be asked to upgrade to the most recent version.  Download the latest [OneLake file explorer](https://go.microsoft.com/fwlink/?linkid=2235671).
