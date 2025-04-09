---
title: Overview of Copilot in Fabric
description: Learn about Copilot in Fabric and Power BI, which brings a new way to transform and analyze data, generate insights, and create visualizations and reports.
author: snehagunda
ms.author: sngun
ms.reviewer: 'guptamaya'
ms.custom:
- copilot-learning-hub
- fabric-cat
ms.topic: conceptual
ms.date: 04/08/2025
no-loc: [Copilot]
ms.collection: ce-skilling-ai-copilot
---

# Overview of Copilot in Fabric

Copilot and other generative AI features in preview bring new ways to transform and analyze data, generate insights, and create visualizations and reports in Microsoft Fabric and Power BI. This article introduces you to Copilot in Fabric and tells you how it works in the different workloads. It also discusses data security and privacy, responsible use, and regional availability.

Copilot in Microsoft Fabric is a generative AI assistive technology that aims to enhance the data analytics experience in the Fabric platform for users. Copilot leverages large-language models (LLMs) that attempt to facilitate user interaction with their data and items in Fabric. People who use Copilot can include people who create, manage, and consume Fabric items, including enterprise developers, self-service users, and business users.

:::image type="content" source="media/copilot-fabric-overview/fabric-copilot-users-diagram.svg" alt-text="Diagram showing how enterprise developers, self-service users, and business users can all use Copilot experiences in Fabric workloads.":::

> [!IMPORTANT]
> Copilot in Fabric aims to *augment* the abilities and intelligence of human users. Copilot can't and doesn't aim to *replace* the people who today create and manage reports or other Fabric items. To get the most out of Copilot in Fabric, you should consider how you'll enable these individuals and teams to make their work more efficient or improve their outcomes.

There are different Copilots in each of the Fabric workloads, like Data Factory, Data Science, and Power BI. Furthermore, Copilot experiences are also available from Power BI Desktop if users have access to a workspace that uses a Fabric capacity with an F64 or higher SKU.

:::image type="content" source="media/copilot-fabric-overview/copilot-fabric-power-bi-diagram.svg" alt-text="Diagram showing how users can use Copilot experiences in Fabric and Power BI Desktop, which both consume Fabric capacity.":::

Enabling and effectively using Copilot in your organization requires deliberate thought and planning. Generative AI is an evolving technology with specific nuances and considerations to keep in mind, so it's important to apply generative AI tools like Copilot to the appropriate problems and scenarios. Furthermore, Copilot in Power BI consumes your available Fabric capacity, meaning that you should manage its usage to avoid overconsumption that can lead to throttling and disruption of your other Fabric operations.

## Enable Copilot

Before your business can start using Copilot capabilities in Microsoft Fabric, you need to [enable Copilot](copilot-enable-fabric.md).

> [!NOTE]
> Copilot is not yet supported for sovereign clouds due to GPU availability.

## Copilot experiences

You can enable and use Copilot across the various Fabric workloads, and within those workloads you can use different Copilot experiences. While each of these Copilot experiences uses a similar common architecture, they work in distinct ways.

The following diagram depicts an overview of the different items that support Copilot experiences for each Fabric workload.

:::image type="content" source="media/copilot-fabric-overview/fabric-items-copilot-support.svg" alt-text="Diagram showing the different Fabric items that support Copilot experiences across Fabric workloads.":::

### Where to find the Copilot experiences in Fabric

The following table provides an overview of the various Copilot experiences available in Fabric, and which workloads and items these experiences apply to. The links in the *Copilot experience* column take you to the documentation describing how to set up and use these features.

:::row:::
   :::column span="1"::: 
**Fabric workload**
   :::column-end:::
   :::column span="1"::: 
**Description**
   :::column-end:::
   :::column span="1"::: 
**Supported items**
   :::column-end:::
   :::column span="1"::: 
**Copilot experience**
   :::column-end:::
:::row-end:::
---
:::row:::
   :::column span="1":::
**Data Science and Data Engineering**
   :::column-end:::
   :::column span="1":::
​Copilot for Data Science and Data Engineering is an AI-powered assistant designed to enhance data professionals' workflows by offering intelligent code completion, automating routine tasks, and providing industry-standard code templates. It integrates with Lakehouse tables, Power BI Datasets, and various dataframes to deliver contextual code suggestions. From data preparation to insight generation, Copilot serves as an interactive aide, streamlining the journey from raw data to meaningful conclusions.
   :::column-end:::
   :::column span="1":::
Notebook (typically with lakehouses and other data items)
   :::column-end:::
   :::column span="1":::
* [Copilot chat panel](../data-engineering/copilot-notebooks-chat-pane.md) vs [chat magics](../data-engineering/copilot-notebooks-chat-magics.md) in a notebook (GA).
* [Generate code or markdown for a notebook (preview)](../data-engineering/copilot-notebooks-chat-pane.md#key-capabilities).
* [Add comments, fix errors, or debug notebook code (preview)](../data-engineering/copilot-notebooks-chat-magics.md#commenting-and-debugging).
* [Analyze and visualize data from a lakehouse, semantic model, or dataframe in the notebook (preview)](../data-engineering/copilot-notebooks-chat-pane.md).
* [Explain notebook contents or activities (preview)](../data-engineering/copilot-notebooks-chat-pane.md#key-capabilities).
   :::column-end:::
:::row-end:::
---

| **Fabric workload** | **Supported items** | **Copilot experience** |  **Description** |
|---|---|---|---|
| **Data Science and Data Engineering** | Notebook (typically with lakehouses and other data items) | * [Copilot chat panel](../data-engineering/copilot-notebooks-chat-pane.md) vs [chat magics](../data-engineering/copilot-notebooks-chat-magics.md) in a notebook (GA).<br/> * [Generate code or markdown for a notebook (preview)](../data-engineering/copilot-notebooks-chat-pane.md#key-capabilities). <br/> * [Add comments, fix errors, or debug notebook code (preview)](../data-engineering/copilot-notebooks-chat-magics.md#commenting-and-debugging).<br/> * [Analyze and visualize data from a lakehouse, semantic model, or dataframe in the notebook (preview)](../data-engineering/copilot-notebooks-chat-pane.md).<br/> * [Explain notebook contents or activities (preview)](../data-engineering/copilot-notebooks-chat-pane.md#key-capabilities). | Copilot for Data Engineering and Data Science is an AI-enhanced toolset tailored to support data professionals in their workflow. It provides intelligent code completion, automates routine tasks, and supplies industry-standard code templates to facilitate building robust data pipelines and crafting complex analytical models. Utilizing advanced machine learning algorithms, Copilot offers contextual code suggestions that adapt to the specific task at hand, helping you code more effectively and with greater ease. From data preparation to insight generation, Microsoft Fabric Copilot acts as an interactive aide, lightening the load on engineers and scientists and expediting the journey from raw data to meaningful conclusions. |
| **Data Factory** | Dataflows gen2 | - [Suggest a new query (preview)](copilot-fabric-data-factory.md).<br>- [Suggest a new transformation step (preview)](copilot-fabric-data-factory.md).<br>- [Summarize a query and applied steps (preview)](copilot-fabric-data-factory.md).<br>- Generate and run a data pipeline.<br>- Summarize a data pipeline.<br>- Troubleshoot pipeline errors. | Copilot for Data Factory is an AI-enhanced toolset that supports both citizen and professional data wranglers in streamlining their workflow. It provides intelligent code generation to transform data with ease and generates code explanations to help you better understand complex tasks. For more information, see [Copilot for Data Factory](copilot-fabric-data-factory.md). |
| **Data Warehousing** | Data warehouse | - [Generate SQL queries (preview)](../data-warehouse/copilot-chat-pane.md).<br>- [Suggest SQL code completions (preview)](../data-warehouse/copilot-code-completion.md).<br>- [Fix code in SQL queries with quick actions (preview)](../data-warehouse/copilot-quick-action.md).<br> - [Explain code in SQL queries with quick actions (preview)](../data-warehouse/copilot-quick-action.md).<br> | Microsoft Copilot for Fabric Data Warehouse is an AI assistant designed to streamline your data warehousing tasks. Key features of Copilot for Warehouse include Natural Language to SQL, code completion, quick actions, and intelligent insights. For more information, see [Copilot for Data Warehouse](../data-warehouse/copilot.md). |
| **Power BI** | Semantic models in Power BI Desktop or Power BI service | - Copilot experiences when developing a data model.<br>   - [Suggest linguistic model synonyms (GA)](/power-bi/natural-language/q-and-a-copilot-enhancements).<br>   - [Suggest measure descriptions (GA)](/power-bi/transform-model/desktop-measure-copilot-descriptions).<br>   - Copilot in TMDL scripting view (announced).<br><br>- Copilot experiences in the DAX query view.<br>   - [Suggest DAX for queries (GA)](/dax/dax-copilot).<br>   - [Suggest DAX for measures (GA)](/dax/dax-copilot).<br>   - [Explain DAX code or concept (GA)](/dax/dax-copilot).<br><br> - Copilot experiences to ask questions about a model.<br>   - Power BI home (announced).<br>   - [Ask questions about your data (preview)](/power-bi/create-reports/copilot-pane-summarize-content). | |
| **Power BI** | Reports (with semantic models) in Power BI Desktop, the Power BI service, or the Power BI mobile app | - Power BI home (announced).<br> - [Suggest a report page (preview)](/power-bi/create-reports/copilot-create-desktop-report).<br>- [Suggest a visual (preview)](/power-bi/create-reports/copilot-create-report-service).<br>- [Summarize data in a narrative visual (GA)](/power-bi/create-reports/copilot-create-narrative?tabs=powerbi-service).<br>- [Explain a report page or visual (GA)](/power-bi/create-reports/copilot-pane-summarize-content). | Power BI has introduced generative AI that allows you to create reports automatically by selecting the topic for a report or by prompting Copilot for Power BI on a particular topic. You can use Copilot for Power BI to generate a summary for the report page that you created, as well as generate synonyms for better Q&A capabilities.<br><br>For more information on the features and how to use Copilot for Power BI, see [Overview of Copilot for Power BI](/power-bi/create-reports/copilot-introduction). |
| **Real-Time Intelligence** | KQL queryset | - [Generate KQL queries (preview)](copilot-real-time-intelligence.md).<br>- [Modify or explore a previously generated KQL query (preview)](copilot-real-time-intelligence.md). | Copilot for Real-Time Intelligence is an advanced AI tool designed to help you explore your data and extract valuable insights. You can input questions about your data, which are then automatically translated into Kusto Query Language (KQL) queries. Copilot streamlines the process of analyzing data for both experienced KQL users and citizen data scientists.<br><br>For more information, see [Copilot for Real-Time Intelligence overview](../fundamentals/copilot-real-time-intelligence.md). |
| **Real-Time Intelligence** | Real-time dashboards | - Generate a real-time dashboard (announced). | |

> [!NOTE]
> Copilot's capabilities are evolving over time. More items and Copilot experiences will likely become available in the future.
>
> The Copilot experiences which are in *preview* are subject to separate, [supplemental preview terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/), and aren't meant for production use. For more information, see [Microsoft Fabric preview information](./preview.md). We recommend that you only use these preview experiences to test and evaluate Copilot's capabilities.

## Create your own AI solution accelerators

### Build your own copilots

Using the [client advisor AI accelerator](https://github.com/microsoft/Build-your-own-copilot-Solution-Accelerator) tool, you can build custom copilot with your enterprise data. The client advisor AI accelerator uses Azure OpenAI Service, Azure AI Search, and Microsoft Fabric to create custom Copilot solutions. This all-in-one custom copilot empowers client advisors to use generative AI across structured and unstructured data optimizing daily tasks and fostering better interactions with clients. To learn more, see the [GitHub repo.](https://github.com/microsoft/Build-your-own-copilot-Solution-Accelerator)

### Conversational knowledge mining solution accelerator

The conversational knowledge mining solution accelerator is built on top of Microsoft Fabric, Azure OpenAI Service, and Azure AI Speech. It enables customers with large amounts of conversational data to use generative AI to find key phrases alongside the operational metrics. This way, you can discover valuable insights with business impact. To learn more, see the [GitHub repo.](https://github.com/microsoft/Customer-Service-Conversational-Insights-with-Azure-OpenAI-Services)

## How do I use Copilot responsibly?

Microsoft is committed to ensuring that our AI systems are guided by our [AI principles](https://www.microsoft.com/ai/principles-and-approach/) and [Responsible AI Standard](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE5cmFl). These principles include empowering our customers to use these systems effectively and in line with their intended uses. Our approach to responsible AI is continually evolving to proactively address emerging issues.

The article [Privacy, security, and responsible use for Copilot (preview)](copilot-privacy-security.md) offers guidance on responsible use.

Copilot features in Fabric are built to meet the Responsible AI Standard, which means that they're reviewed by multidisciplinary teams for potential harms, and then refined to include mitigations for those harms.  

Before you use Copilot, your admin needs to enable Copilot in Fabric. See the article [Overview of Copilot in Fabric](copilot-fabric-overview.md) for details. Also, keep in mind the limitations of Copilot:

- Copilot responses can include inaccurate or low-quality content, so make sure to review outputs before using them in your work.
- Reviews of outputs should be done by people who are able to meaningfully evaluate the content's accuracy and appropriateness.
- Today, Copilot features work best in the English language. Other languages might not perform as well.

## Available regions

### Available regions for Azure OpenAI Service

To access the prebuilt [Azure OpenAI Service](https://azure.microsoft.com/products/ai-services/openai-service/), including the [Copilot in Fabric](copilot-fabric-overview.md), you must have an F64 or higher SKU or a P SKU in the following [Fabric regions](../admin/region-availability.md). The Azure OpenAI Service isn't available on trial SKUs.

The Azure OpenAI Service used to power Fabric Copilot is currently deployed only in US datacenters (East US, East US2, South Central US, and West US) and one EU datacenter (France Central). This differs from the standard Azure OpenAI Service available in the Azure portal, which is accessible in many more regions. For details on standard Azure OpenAI region availability, see [Azure OpenAI Service region availability](/azure/ai-services/openai/concepts/models?tabs=global-standard%2Cstandard-chat-completions#model-summary-table-and-region-availability). If your data is outside the US or EU, the feature is disabled by default unless your tenant admin enables **Data sent to Azure OpenAI can be processed outside your capacity's geographic region, compliance boundary, or national cloud instance** tenant setting. To learn how to get to the tenant settings, see [About tenant settings](../admin/service-admin-portal-copilot.md).

### Data processing across geographic areas

The prebuilt [Azure OpenAI Service](https://azure.microsoft.com/products/ai-services/openai-service/) and [Copilot in Fabric](copilot-fabric-overview.md) might process your prompts and results (input and output when using Copilot) outside your capacity's geographic region, depending on where the Azure OpenAI service is hosted. The table below shows the mapping of where data is processed across geographic areas for Copilot in Fabric and Azure OpenAI features.  

> [!NOTE]
> The data processed for Copilot interactions can include user prompts, meta prompts, structure of data (schema) and conversation history. No data, such as content in tables is sent to Azure OpenAI for processing unless specifically directed by the user.

|Geographic area where your Fabric Capacity is located |Geographic area where Azure OpenAI Service is hosted |Data processing outside your capacity's geographic region? |Actions required to use Fabric Copilot |
|-|-|-|-|
|US |US |No |Turn on Copilot. |
|EU Data Boundary |EU Data Boundary |No |Turn on Copilot. |
|UK |EU Data Boundary |Yes |Turn on Copilot.<br>Enable cross-geo data processing. |
|Australia<br>Brazil<br>Canada<br>India<br>Asia<br>Japan<br>Korea<br>South Africa<br>Southeast Asia<br>United Arab Emirates |US |Yes |Turn on Copilot.<br>Enable cross-geo data processing. |

## Related content

- [What is Microsoft Fabric?](../fundamentals/microsoft-fabric-overview.md)
- [Copilot for Microsoft Fabric and Power BI: FAQ](copilot-faq-fabric.yml)
- [AI services in Fabric (preview)](../data-science/ai-services/ai-services-overview.md)
- [Copilot tenant settings](../admin/service-admin-portal-copilot.md)
