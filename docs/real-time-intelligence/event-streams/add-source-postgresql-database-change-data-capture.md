---
title: Add PostgreSQL Database CDC source to an eventstream
description: Learn how to add a PostgreSQL Database Change Data Capture (CDC) source to an eventstream.
ms.reviewer: spelluru
ms.author: zhenxilin
author: alexlzx
ms.topic: how-to
ms.custom:
  - ignite-2024
ms.date: 11/18/2024
ms.search.form: Source and Destination
---

# Add PostgreSQL Database CDC source to an eventstream

This article shows you how to add a PostgreSQL Database Change Data Capture (CDC) source to an eventstream.

The PostgreSQL Database Change Data Capture (CDC) source connector for Microsoft Fabric event streams allows you to capture a snapshot of the current data in a PostgreSQL database. The connector then monitors and records any future row-level changes to this data. Once the changes are captured in the eventstream, you can process this CDC data in real-time and send it to different destinations within Fabric for further processing or analysis.

[!INCLUDE [new-sources-regions-unsupported](./includes/new-sources-regions-unsupported.md)]

## Prerequisites

- Access to a workspace in the Fabric capacity license mode (or) the Trial license mode with Contributor or higher permissions. 
- Registered user access in the PostgreSQL database.
- Your PostgreSQL database must be publicly accessible and not be behind a firewall or secured in a virtual network.
- CDC enabled in the PostgreSQL database and tables.

  If you have Azure Database for PostgreSQL, follow the steps in the next section to enable CDC. For detailed information, see [Logical replication and logical decoding - Azure Database for PostgreSQL - Flexible Server](/azure/postgresql/flexible-server/concepts-logical).

  For other PostgreSQL databases, see [Debezium connector for PostgreSQL :: Debezium Documentation](https://debezium.io/documentation/reference/stable/connectors/postgresql.html#setting-up-postgresql).
- If you don't have an eventstream, [create an eventstream](create-manage-an-eventstream.md). 

## Enable CDC in your Azure Database for PostgreSQL

To enable CDC in your **Azure Database for PostgreSQL Flexible Server**, follow these steps:

1. On your Azure Database for PostgreSQL Flexible Server page in the Azure portal, select **Server parameters** in the navigation menu.

1. On the **Server parameters** page:

   - Set **wal_level** to **logical**.
   - Update the **max_worker_processes** to at least **16**.

   :::image type="content" border="true" source="media/add-source-postgresql-database-cdc-connector/enable-cdc-flexible.png" alt-text="A screenshot of enabling CDC for a flexible server deployment.":::

1. Save the changes and restart the server.

1. Confirm that your Azure Database for PostgreSQL Flexible Server instance allows public network traffic.

1. Grant the **admin user** replication permissions by running the following SQL statement. If you want to use other user account to connect your PostgreSQL DB to fetch CDC, please ensure the user is the **table owner**.

   ```sql
   ALTER ROLE <admin_user_or_table_owner_user> WITH REPLICATION;
   ```

## Launch the Select a data source wizard
[!INCLUDE [launch-connect-external-source](./includes/launch-connect-external-source.md)]

On the **Select a data source** page, search for and select **Connect** on the **Azure DB for PostgreSQL (CDC)** tile.

:::image type="content" source="./media/add-source-postgresql-database-cdc-connector/select-postgresql-cdc.png" alt-text="Screenshot that shows the selection of Azure DB for PostgreSQL (CDC) as the source type in the Get events wizard." lightbox="./media/add-source-postgresql-database-cdc-connector/select-postgresql-cdc.png":::

## Configure and connect to Azure Database for PostgreSQL CDC

[!INCLUDE [postgresql-database-cdc-connector](./includes/postgresql-database-cdc-source-connector.md)]

[!INCLUDE [sources-destinations-note](./includes/sources-destinations-note.md)]

## View updated eventstream

1. You can see the PostgreSQL Database CDC source added to your eventstream in **Edit mode**.

    :::image type="content" source="media/add-source-postgresql-database-cdc-connector/edit-view.png" alt-text="A screenshot of streaming PostgreSQL DB CDC source in Edit view." lightbox="media/add-source-postgresql-database-cdc-connector/edit-view.png":::
1. To implement this newly added PostgreSQL DB CDC source, select **Publish**. After you complete these steps, your PostgreSQL DB CDC source is available for visualization in the **Live view**.

    :::image type="content" source="media/add-source-postgresql-database-cdc-connector/live-view.png" alt-text="A screenshot of streaming PostgreSQL DB CDC source in Live view." lightbox="media/add-source-postgresql-database-cdc-connector/live-view.png":::

## Related content

Other connectors:

- [Amazon Kinesis Data Streams](add-source-amazon-kinesis-data-streams.md)
- [Azure Cosmos DB](add-source-azure-cosmos-db-change-data-capture.md)
- [Azure Event Hubs](add-source-azure-event-hubs.md)
- [Azure Service Bus](add-source-azure-service-bus.md)
- [Azure IoT Hub](add-source-azure-iot-hub.md)
- [Azure SQL Database Change Data Capture (CDC)](add-source-azure-sql-database-change-data-capture.md)
- [Confluent Kafka](add-source-confluent-kafka.md)
- [Custom endpoint](add-source-custom-app.md)
- [Google Cloud Pub/Sub](add-source-google-cloud-pub-sub.md) 
- [MySQL Database CDC](add-source-mysql-database-change-data-capture.md)
- [PostgreSQL Database CDC](add-source-postgresql-database-change-data-capture.md)
- [Sample data](add-source-sample-data.md)
- [Azure Blob Storage events](add-source-azure-blob-storage.md)
- [Fabric workspace event](add-source-fabric-workspace.md)
