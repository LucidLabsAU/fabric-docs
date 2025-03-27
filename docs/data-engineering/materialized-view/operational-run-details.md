---
title: Understand DAG UI operational run details
description: Learn how to understand DAG UI operational run details
ms.topic: how-to
author: apurbasroy
ms.author: apsinhar
ms.reviewer: nijelsf
ms.date: 03/27/2025
---

# Understand DAG UI operational run details

Operational run details encompass the various parameters and metrics tracked during the execution of a materialized view DAG.

## Activity Panel

The Activity Panel is the  bottom panel where user can get the information of the following:

*	Materialized Views which are a part of the DAG
*	The Status of the DAG
*	The Start time of the DAG
*	The Duration of the DAG
*	Search Bar for the nodes

**Image1**

User can click on any node in the DAG UI or the Materialized View name in the Activity Panel
to zoom in on the end to end flow of a particular node.

**Image2**

## Details Panel

The Details Panel on the right side of the DAG UI contains the node level information and is completely available once the
user clicks on a particular node. The Details panel has the following information:

*	Name of the node
*	Type of node
*	Start Time
*	Completion Time
*	Duration
*	Status
*	Detailed Logs with link to Monitoring hub for debugging

**Image3**

On clicking the **More Details** link, the user is navigated to the Monitoring Hub Page for job level monitoring.

## Next Steps

  

