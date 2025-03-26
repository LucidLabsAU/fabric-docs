---
title: "Microsoft Fabric materialized views tutorial"
description: This tutorial outlines the steps and considerations for implementing a medallion architecture for a sales analytics pipeline Fabric materialized views.
ms.author: rkottackal 
author: rkottackal 
ms.reviewer: nijelsf
ms.topic: tutorial
ms.date: 03/26/2025
---

# Microsoft Fabric materialized views tutorial
This tutorial outlines the steps and considerations for implementing a medallion architecture for a sales analytics pipeline Fabric materialized views. By the end of this tutorial, you'll understand the key features and capabilities of Fabric materialized views and be able to create an automated data transformation workflow.
## Overview
Fabric materialized views are designed to simplify the implementation of the Medallion architecture using Spark SQL. These views allow for automated creation, scheduling, and execution of materialized views, optimizing data transformations through a declarative approach. Fabric materialized views offers declarative pipelines, manages dependencies, automates data processing workflows, and  robust monitoring capabilities to help data professionals in their data transformation journey.

## Key features and benefits
*	**Declarative pipelines**: They help manage data transformations through a declarative approach, optimizing execution as opposed to manually setting up and managing pipelines individually.
*	**Data quality checks**: Users can define and implement data quality checks and actions to be taken on errors, ensuring high data quality.
*	**Performance optimization**: The processing pipeline can optimize for performance by identifying the right sequence to update the data, only refreshing segments of the DAG that have changes.
*	**Visualization and monitoring**: Developers can create and monitor data pipelines using SQL syntax extensions, visualize the directed acyclic graph (DAG) of the pipeline, and track its performance and status.

## Medallion architecture for sales analytics use case

:::image type="content" source="./media/tutorial/sales-lakehouse.png" alt-text="Screenshot showing medallion architecture." border="true" lightbox="./media/tutorial/sales-lakehouse.png":::

:::image type="content" source="./media/tutorial/maintain-pipeline.png" alt-text="Screenshot showing challenges in maintaining pipeline." border="true" lightbox="./media/tutorial/maintain-pipeline.png":::

**Layers**
* Bronze Layer: Ingests raw data
* Silver Layer: Cleanses data
* Gold Layer: Curates data for analytics and reporting

## Creating a pipeline

The high-level steps in module 1 are as follows:
1. **Bronze Layer**: Ingests raw data in the form of CSV files using Load to Table.
1. **Silver Layer**: Cleanses data using Fabric materialized views
1. **Gold Layer**: Curates data for analytics and reporting using Fabric materialized views.

As prerequisites to this tutorial, complete the following steps:
1.	Sign into your Power BI online account, or if you don't have an account yet, sign up for a free trial.
1.	Enable Microsoft Fabric in your tenant. Select the default Power BI icon at the bottom left of the screen and select Fabric.
1.	Create a Microsoft Fabric enabled Workspace: Create a workspace.
1.	Select a workspace from the Workspaces tab, then select + New item, and choose Data engineering. Provide a pipeline name. Then select Create.
1.	Create a Lakehouse titled SalesLakehouse and load the sample data files for raw data into the Lakehouse. For more information, see [Lakehouse tutorial](/fabric/data-engineering/tutorial-build-lakehouse).

**Sample Data**

Contoso is leveraging a medallion architecture for data analytics to gain actionable insights into its retail sales operations. Contoso aims to streamline the analysis process and generate deeper insights into business performance by organizing their data into three layers—bronze (raw data), silver (cleaned and enriched data), and gold (aggregated and analyzed data).

**Entities**
1.	**Orders**: This entity includes details about each customer order, such as order date, shipment details, product category, and subcategory. Insights can be drawn to optimize shipping strategies, identify popular product categories, and improve order management.
1.	**Sales**: By analyzing sales data, Contoso can assess key metrics like total revenue, profit margins, order priorities, and discounts. Correlations between these factors provide a clearer understanding of customer purchasing behaviors and the efficiency of discount strategies.
1.	**Location**: This captures the geographical dimension of sales and orders, including cities, states, regions, and customer segments. It helps Contoso identify high-performing regions, address low-performing areas, and personalize strategies for specific customer segments.
1.	**Agent performance**: With details on agents managing transactions, their commissions, and sales data, Contoso can evaluate individual agent performance, incentivize top performers, and design effective commission structures.
1.	**Agent commissions**: Incorporating commission data ensures transparency and enables better cost management. Understanding the correlation between commission rates and agent performance helps refine incentive systems.

**Dataset**

Contoso has the raw data of its retail operations stored in CSV format at ADLS Gen2. Contoso hopes to leverage these to create the bronze layer of medallion architecture. It has created Spark SQL commands in a Notebook to create Fabric materialized views forming the silver and gold layers of the medallion architecture. 
Note: these data models and reports aren't yet available,

## Create bronze layer of Sales Analytics Medallion Architecture

1.	Load the CSV files into the Lakehouse. For more information, see [Options to get data into the Lakehouse](/fabric/data-engineering/load-data-lakehouse).
1.	Create a bronze schema. For more information, see [Lakehouse schemas](/fabric/data-engineering/lakehouse-schemas#create-a-lakehouse-schema).
1.	Convert the raw CSV files into delta tables using Load to Table. For more information, see [Lakehouse Load to Delta Lake tables](/fabric/data-engineering/load-to-tables).

    :::image type="content" source="./media/tutorial/notebook-table.png" alt-text="Screenshot showing notebook." border="true" lightbox="./media/tutorial/notebook-table.png":::

## Create silver and gold layers of Sales Analytics Medallion Architecture

1.	Download the Notebook file and upload it to your workspace.

    :::image type="content" source="./media/tutorial/create-silver-layer.png" alt-text="Screenshot showing silver materialized view creation." border="true" lightbox="./media/tutorial/create-silver-layer.png":::

1.	Open the Notebook from the Lakehouse.  For more information, see [Explore the lakehouse data with a notebook](/fabric/data-engineering/lakehouse-notebook-explore). 

  	:::image type="content" source="./media/tutorial/create-bronze-layer.png" alt-text="Screenshot showing creating bronze layer." border="true" lightbox="./media/tutorial/create-bronze-layer.png":::

1.	Run all cells of the notebook using Spark SQL to create Fabric materialized views with data quality constraints. Once all cells are successfully executed, you can refresh the Saleslakehouse source to view the newly created Materialized Views for silver and gold schema.

  	:::image type="content" source="./media/tutorial/run-notebook.png" alt-text="Screenshot showing run notebook." border="true" lightbox="./media/tutorial/run-notebook.png":::

## Automating the pipeline

1.	Once the materialized views for silver and gold layers are created, click on the ‘Managed Materialized View’ button in the Lakehouse to view the plain directed acyclic graph (DAG) autogenerated based on dependencies. You can find that each dependent materialized view form a node of the DAG.

  	:::image type="content" source="./media/tutorial/managed-materialized-view-1.png" alt-text="Screenshot showing materialized view." border="true" lightbox="./media/tutorial/managed-materialized-view-1.png":::

  	:::image type="content" source="./media/tutorial/managed-materialized-view-2.png" alt-text="Screenshot showing creation of dag." border="true" lightbox="./media/tutorial/managed-materialized-view-2.png":::

1.	Turn on and configure schedule run for the DAG.

  	:::image type="content" source="./media/tutorial/run-dag.png" alt-text="Screenshot showing scheduling run dag." border="true" lightbox="./media/tutorial/run-dag.png":::

## Monitoring and Troubleshooting
1.	The dropdown menu will list the current and historical DAG runs. 

  	:::image type="content" source="./media/tutorial/dropdown-menu.png" alt-text="Screenshot showing scheduling dag execution." border="true" lightbox="./media/tutorial/dropdown-menu.png":::

1.	By clicking on the latest run, you can find the DAG metrics on right side panel. The bottom activity panel will provide a high-level overview of node execution status.

  	:::image type="content" source="./media/tutorial/latest-run.png" alt-text="Screenshot showing latest run." border="true" lightbox="./media/tutorial/latest-run.png":::

1.	Clicking on any node in the DAG will provide the node execution details and link to detailed logs.

  	:::image type="content" source="./media/tutorial/execution details.png" alt-text="Screenshot showing execution details." border="true" lightbox="./media/tutorial/execution details.png":::

1.	If the node status is “Failed”, then the error message will also be displayed.

  	:::image type="content" source="./media/tutorial/execution-detail-logs.png" alt-text="Screenshot showing execution detail logs." border="true" lightbox="./media/tutorial/execution-detail-logs.png":::

1.	Clicking on the Detailed logs link will redirect you to the Monitoring Hub from where you can access Spark error logs for further troubleshooting.

  	:::image type="content" source="./media/tutorial/spark-logs.png" alt-text="Screenshot showing spark logs." border="true" lightbox="./media/tutorial/spark-logs.png":::

**Future Enhancements**
*	Built-in data quality dashboard.
*	PySpark support for materialized views.
*	Incremental refresh of materialized views.
*	Creation of live tables using extended SQL.
*	Data quality alerts.

## Next steps
