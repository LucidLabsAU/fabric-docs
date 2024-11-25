---
title: "SQL database Overview (Preview)"
description: Learn about SQL database in Microsoft Fabric.
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.reviewer: antho, sukkaur
ms.date: 11/07/2024
ms.topic: overview
ms.custom:
  - ignite-2024
ms.search.form: product-databases
---
# SQL database in Microsoft Fabric (Preview)

**Applies to:** [!INCLUDE [fabric-sqldb](../includes/applies-to-version/fabric-sqldb.md)]

SQL database in Microsoft Fabric is a developer-friendly transactional database, based on [Azure SQL Database](/azure/azure-sql/database/sql-database-paas-overview?view=azuresqldb-current&preserve-view=true), that allow you to easily create your operational database in Fabric. A SQL database in Fabric uses the same SQL Database Engine as Azure SQL Database.

[!INCLUDE [feature-preview-note](../../includes/feature-preview-note.md)]

To get started, see the tutorial to [Create a SQL database in the Fabric portal](create.md).

SQL database in Fabric is:

- The home in Fabric for OLTP workloads
- Easy to configure and manage
- Set up for analytics by automatically replicating the data into OneLake near real time
- Integrated with development frameworks and analytics
- Based on the underlying technology of [Mirroring in Fabric](../mirrored-database/overview.md)
- Queried in all the same ways as [Azure SQL Database](/azure/azure-sql/database/sql-database-paas-overview?view=azuresqldb-current&preserve-view=true), plus a [web-based editor in the Fabric portal](query-editor.md).

Intelligent performance features from Azure SQL Database are enabled by default in SQL database in Fabric, including:

- [Automatic index creation with Automatic Tuning](/azure/azure-sql/database/automatic-tuning-overview?view=azuresql-db&preserve-view=true)

[!INCLUDE [feature-preview-note](../../includes/feature-preview-note.md)]

## Why use SQL database in Fabric?

SQL database in Fabric is part of the **Database** workload, and the data is accessible from other items in Fabric. Your SQL database data is also kept up-to-date in a queryable format in OneLake, so you can use all the different services in Fabric, such as running analytics with Spark, executing notebooks, data engineering, visualizing through Power BI Reports, and more.

:::image type="content" source="media/overview/sql-database.png" alt-text="A screenshot of the SQL database icon in Fabric.":::

With your SQL database in Fabric, you don't need to piece together different services from multiple vendors. Instead, you can enjoy a highly integrated, end-to-end, and easy-to-use product that is designed to simplify your analytics needs, and built for openness and collaboration between technology solutions that can read the open-source Delta Lake table format. The Delta tables can then be used everywhere in Fabric, allowing users to accelerate their journey into Fabric.

The Microsoft Fabric platform is built on a foundation of Software as a Service (SaaS). To learn more about Microsoft Fabric, see [What is Microsoft Fabric?](../../get-started/microsoft-fabric-overview.md)

SQL database in Fabric creates three items in your Fabric workspace:

- Data in your SQL database is automatically replicated of into the [OneLake](../../onelake/onelake-overview.md) and converted to Parquet, in an analytics-ready format. This enables downstream scenarios like data engineering, data science, and more.

- A SQL analytics endpoint
- A default semantic model

In addition to the [Fabric SQL database Query Editor](query-editor.md), there's a broad ecosystem of tooling including [SQL Server Management Studio](/sql/ssms/download-sql-server-management-studio-ssms), [the mssql extension with Visual Studio Code](/sql/tools/visual-studio-code/mssql-extensions?view=fabric&preserve-view=true), and even GitHub Copilot.

## Sharing

Sharing enables ease of access control and management, while security controls like row level security (RLS) and object level security (OLS), and more make sure you can control access to sensitive information. Sharing also enables secure and democratized decision-making across your organization.

By sharing your SQL database, you can grant other users or a group of users access to a database without giving access to the workspace and the rest of its items. When someone shares a database, they also grant access to the SQL analytics endpoint and associated default semantic model.

Access the Sharing dialog with the **Share** button next to the database name in the **Workspace** view. Shared databases can be found through **OneLake** **Data Hub** or the **Shared with Me** section in Microsoft Fabric.

For more information, see [Share data and manage access to your SQL database in Microsoft Fabric](share-data.md).

## Connect

Like other Microsoft Fabric item types, SQL databases rely on [Microsoft Entra authentication](/entra/identity/authentication/overview-authentication). For options to connect, review [Connect to your SQL database in Microsoft Fabric](connect.md).

To successfully authenticate to a SQL database, a Microsoft Entra user, a [service principal](/entra/identity-platform/app-objects-and-service-principals), or their [group](/entra/fundamentals/concept-learn-about-groups), must have the Read item permission for the database in Fabric.
For more information, see [Authentication in SQL database in Microsoft Fabric](authentication.md).

- For information on how to grant a Microsoft Entra identity access to a Fabric workspace or a specific database, see [Fabric access controls](authorization.md#fabric-access-controls).

## Cross-database queries

With the data from your SQL database automatically stored in the OneLake, you can write cross-database queries, joining data from other SQL databases, mirrored databases, warehouses, and the SQL analytics endpoint in a single T-SQL query. All this is currently possible with queries on the SQL analytics endpoint of the SQL database, or lakehouse.

For example, you can reference a table from other items in Fabric using three-part naming. In the following example, use the three-part name to refer to `ContosoSalesTable` in the warehouse `ContosoWarehouse` from the fictional `SalesLT.Affiliation` table in a SQL database. From other databases or warehouses, the first part of the standard SQL three-part naming convention is the name of the database or warehouse item.

```sql
SELECT * 
FROM ContosoWarehouse.dbo.ContosoSalesTable AS Contoso
INNER JOIN AdventureWorksLT.SalesLT.Affiliation AS Affiliation
ON Affiliation.AffiliationId = Contoso.RecordTypeID;
```

## Data Engineering with your SQL database in Fabric

Microsoft Fabric provides various data engineering capabilities to ensure that your data is easily accessible, well-organized, and high-quality. From [Fabric Data Engineering](../../data-engineering/data-engineering-overview.md), you can:

- Create and manage your data as Spark using a SQL database in Fabric.
- Design pipelines to copy data into your SQL database in Fabric.
- Use Spark job definitions to submit batch/streaming job to Spark cluster.
- Use notebooks to write code for data preparation and transformation.

## Data Science with your SQL database in Fabric

Data Science in Microsoft Fabric to empower users to complete end-to-end data science workflows for the purpose of data enrichment and business insights. You can complete a wide range of activities across the entire data science process, all the way from data exploration, preparation and cleansing to experimentation, modeling, model scoring and serving of predictive insights to BI reports.

Microsoft Fabric users can access [Data Science](../../data-science/data-science-overview.md). From there, they can discover and access various relevant resources. For example, they can create machine learning Experiments, Models and Notebooks. They can also import existing Notebooks on the Data Science Home page.

## Database portability and deployments with SqlPackage

SqlPackage is a cross-platform command line tool that enables database interactions that move entire databases or database objects. The portability (import/export) of a database managed in Azure or in Fabric ensures that your data is portable should you want to migrate later on. The same portability also enables certain migration scenarios through self-contained database copies (.bacpac) with import/export operations.

SqlPackage can enable easy database deployments of incremental changes to database objects (new columns in tables, alterations to existing stored procedures, etc.). SqlPackage can extract a .dacpac file containing the definitions of objects in a database, and publish a .dacpac file to apply that object state to a new or existing database. The publish operation also integrates with SQL projects, which enables offline and more dynamic development cycles for SQL databases.

For more information, see [SqlPackage with SQL database in Fabric](sqlpackage.md).

## Integration with Fabric source control

SQL database is integrated with [Fabric continuous integration/continuous development](../../cicd/cicd-overview.md). You can use the built-in git repository to manage your SQL database.

## Create GraphQL API from Fabric portal

You can use the Fabric portal to easily [create a GraphQL API](graphql-api.md) for your SQL database.

## Capacity management

You can use the [Microsoft Fabric Capacity Metrics app](../../enterprise/metrics-app.md) to monitor the SQL database usage and consumption in non-trial Fabric capacities.

> [!NOTE]
> During the current preview, no billing will occur for SQL database in Fabric, but billing metrics will still flow for tracking purposes.

## Mirroring for Azure SQL Database

Do you already have an external database and want to leverage Fabric's integration? You can use Mirroring in Fabric as a low-cost and low-latency solution to bring data from various systems together. You can continuously replicate your existing data estate directly into Fabric's OneLake, including data from an existing [Azure SQL Database](../mirrored-database/azure-sql-database.md).

## Next step

> [!div class="nextstepaction"]
> [Create a SQL database in the Fabric portal](create.md)

## Related content

- [What is Microsoft Fabric?](../../get-started/microsoft-fabric-overview.md)
- [Frequently asked questions for SQL database in Microsoft Fabric (preview)](faq.yml)
- [What is the SQL analytics endpoint for a Lakehouse?](../../data-engineering/lakehouse-sql-analytics-endpoint.md)
- [Direct Lake](/power-bi/enterprise/directlake-overview)
