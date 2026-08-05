---
title: 迁移到 [!DNL Adobe Commerce as a Cloud Service]
description: 了解如何迁移到 [!DNL Adobe Commerce as a Cloud Service]。
feature: Cloud
exl-id: 9065c92a-f6b2-4464-8ec0-5c549bf78104
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目（Adobe管理的SaaS基础架构）。"
role: Developer
level: Intermediate
autotag-review: '2026-06-18T16:12:28.840Z'
TQID: 'https://experienceleague.adobe.com/GmxaQdGKvAIDpZ2jvmlLFSYw0IFQysIMOT0lUnsJBsI'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
subfeature_v2:
  - id: e91a50b1-0b31-436e-9033-00e4776e94cb
  - id: f56d26ed-050b-4fb7-b29b-8e6e994e80a2
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: addc3a3a-2b1c-4fdf-aea4-4b1eb2931ba6
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: e03840ea9e0e43a005f385914e8599804383e79d
workflow-type: tm+mt
source-wordcount: 3305
ht-degree: 0%

---

# 迁移到[!DNL Adobe Commerce as a Cloud Service]

本指南帮助开发人员从[!DNL Adobe Commerce on Cloud]或内部部署迁移到[!DNL Adobe Commerce as a Cloud Service] (SaaS)。 此SaaS模型提供了增强的性能、可扩展性以及与[!DNL Adobe Experience Cloud]的集成。

>[!NOTE]
>
>有关迁移工具的详细信息，请参阅[批量数据迁移工具](./bulk-data/migration-tool.md)。

## 概述

将已建立的[!DNL Adobe Commerce]存储迁移到[!DNL Adobe Commerce as a Cloud Service]不仅仅是移动数据。 真正的迁移跨以下区域：

- 应用程序 — 为[!DNL Adobe Commerce on Cloud]或内部安装构建的自定义项和扩展
- 数据 — 目录、订单、客户和配置
- 店面
- 与外部系统集成

[!DNL Adobe Commerce as a Cloud Service]是一个无版本的SaaS平台，这意味着这些区域都不能在不调整它们的情况下进行迁移。 自定义已现代化到[!DNL App Builder]应用程序中，在Edge Delivery Services (EDS)上重建了店面，数据迁移到了新的[!DNL Adobe Commerce as a Cloud Service]租户，并且使用SaaS模式重新建立了集成。

Adobe提供了围绕[三个迁移工具](#migration-tools-workflow)构建的集成迁移工作流，而不是将迁移视为单个整体项目。

此共享工作流可整合发现、协调工程团队和交付团队，并提供一致的迁移计划。

![迁移流程图](../assets/migration-flow.png)

### PaaS和SaaS比较

[!DNL Adobe Commerce on Cloud]或内部部署(PaaS)和[!DNL Adobe Commerce as a Cloud Service] (SaaS)的管理方式以及商家与平台的交互方式有所不同。

**主要差异**

- 仅[!BADGE PaaS]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于云项目（Adobe管理的PaaS基础架构）和内部部署项目上的Adobe Commerce 。"}
- **[!DNL Adobe Commerce on Cloud Infrastructure]**：商家管理应用程序代码、升级、修补和基础结构配置。
- **[!DNL Adobe Commerce]本地**：商家在Adobe的托管环境中管理应用程序代码、升级、修补和基础架构配置。

  >[!NOTE]
  >
  >[共享责任模型](https://experienceleague.adobe.com/en/docs/commerce-operations/security-and-compliance/shared-responsibility)，适用于服务（MySQL、Elasticsearch等）。

- [!BADGE 仅限SaaS]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目（Adobe管理的SaaS基础架构）。"} **SaaS（新增 — [!DNL Adobe Commerce as a Cloud Service]）**： Adobe完全管理核心应用程序、基础架构和更新。 商家专注于通过可扩展性点(API、App Builder、UI SDK)进行自定义。 核心应用程序代码已锁定。

**架构影响**

- **无版本平台**：持续更新意味着核心不再进行主要版本升级。
- **微服务和API优先**：更加依赖于API来实现可扩展性和集成。
- **默认为Headless（可选）**：对分离店面的强大支持（例如，由Edge Delivery Services提供支持的Commerce Storefront）。
- **Edge Delivery Services**：对前端性能和部署的影响。

**新工具和概念**

- Adobe Developer App Builder的[Adobe Developer App Builder](https://developer.adobe.com/app-builder/)和[API Mesh](https://developer.adobe.com/graphql-mesh-gateway/)
- [Commerce Optimizer](../../optimizer/overview.md)
- [Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/)
- 使用[Commerce Cloud Manager](../getting-started.md#create-an-instance)进行自助配置

### 迁移历程

迁移将经历以下阶段：

- **评估** — 分析现有实施并考虑以下内容：库存自定义、集成、店面特征和数据结构。 分析之后，创建包含迁移建议、复杂性评分和工作量估计的路线图。
- **使应用程序现代化并迁移数据** — 将业务数据迁移到[!DNL Adobe Commerce as a Cloud Service]时，重新生成自定义项作为[!DNL App Builder]应用程序。
- **使店面现代化** — 在Edge Delivery Services (EDS)上为Commerce重建店面。
- **切换并运行** — 将流量切换到[!DNL Adobe Commerce as a Cloud Service]，停用旧系统，并转换为正在进行的操作。

迁移通常是迭代的，而不是线性的。 组织可以评估多个环境、验证推荐、逐步实现现代化并在最终生产转换之前优化实施计划。

### 迁移工具工作流程

以下每个工作流都有自己的工具。 将这两个功能结合使用来完成迁移，迁移评估将用作整个迁移过程中使用的通用蓝图。

| 工作流 | 工具 | 描述 |
| --- | --- | --- |
| [评估](#migration-assessment-tool) | **迁移评估工具** | AI驱动的现有实施评估，其中清点自定义模块、第三方扩展、集成、店面观察、数据库模式、自定义表、迁移建议、复杂性评分和现代化工作估计值。 |
| [应用程序和店面现代化](#code-and-storefront-migration-commerce-developer-mcp) | **Commerce开发人员MCP** | 人工智能辅助的Commerce应用程序现代化，加快将自定义项迁移到[!DNL App Builder]，支持店面迁移到Edge Delivery Services (EDS)，并通过由工程团队审查和验证的实施指导开发人员完成更广泛的应用程序现代化历程。 |
| [数据迁移](#data-migration-commerce-data-migration-service) | **Commerce数据迁移服务** | 将目录、客户和订单数据的提取、加载和完整性验证到[!DNL Adobe Commerce as a Cloud Service]。 |

这些磁道不是独立的。 以正确的顺序一起使用它们可最大程度地减少重复工作。

- **首先运行评估** — 运行评估首先会识别不支持的自定义项、估计迁移工作量、公开数据迁移注意事项，并在实施开始之前突出显示集成依赖项。 评估将成为应用程序现代化工作流程和数据迁移工作流使用的迁移蓝图。
- **应用程序现代化** - Commerce开发人员MCP使用迁移评估来确定哪些自定义项要现代化以及如何现代化。 然后，MCP生成相应的[!DNL App Builder]应用程序和店面组件。
- **数据迁移** — 数据迁移范围界定调查表捕获评估所显示的范围、卷和自定义表。
- **自定义数据和第三方数据** — 评估期间识别了第三方扩展保存在自定义表中的数据，但标准数据迁移无法处理这些数据，因此需要[!DNL App Builder]自定义。

店面现代化不只是UI迁移。 除了迁移业务功能外，您还需要考虑体验架构、可重用组件现代化、性能优化和Edge Delivery Services模式的采用。

集成将作为迁移评估的一部分进行评估，但其实施因方案而异。 集成可利用[!DNL App Builder]、[!DNL API Mesh]、Adobe I/O Events和[!DNL Adobe Commerce as a Cloud Service] API。

这些迁移工具将继续扩展和维护以迁移评估为中心的统一迁移工作流。

### 后续步骤

准备好迁移后，从创建评估开始。 迁移评估将制定迁移后的计划。

迁移评估工具和Commerce开发人员MCP使用AI帮助您发现、规划和实施。 与任何工程工作流一样，作为标准架构、测试和质量保证流程的一部分，您的团队应该仔细审查和验证AI生成的建议和实施。

## 迁移评估工具

在开始开发或迁移之前，您必须考虑迁移的大小并确定需要开发的项目。 [!DNL Adobe Commerce on Cloud]或内部部署上的[!DNL Adobe Commerce]存储可能具有自定义模块、集成、店面自定义和数据结构，在有人分析实施之前，这些内容可能并不明显。 迁移评估工具会自动扫描您的代码库，以识别这些要开发的项目。

### 评估概述

迁移评估工具对现有实施执行AI评估，并生成结构化现代化评估和[!DNL Adobe Commerce as a Cloud Service]迁移路线图。 它还通过评估应用程序自定义、集成、数据结构、店面特征以及影响现代化的其他实施详细信息，构建迁移的综合视图。 它将发现变成一个快速、可重复的过程，允许您在作出承诺之前评估工作量、风险和排序。

迁移评估工具产生的评估不仅仅是一份报告。 评估将成为共享迁移对象，在整个迁移生命周期内为规划、实施和验证提供信息。 作为迁移历程的第一阶段，其调查结果将同时涵盖应用程序现代化以及随后的数据迁移工作。

有关迁移评估报告中包含的内容及其使用方法的详细信息，请参阅[迁移评估](./assessment.md)。

### 评估阶段

评估将针对现有实施运行，并经历一系列自动化阶段：

- **库存** — 将实施编目。 包括：自定义模块、编辑器依赖项、第三方扩展、配置、店面组件（如果适用）、文件、扩展性点、事件、插件、API、cron作业、队列、数据库模式和自定义数据库表。
- **分析** — 执行静态分析以识别存储自定义项、与标准[!DNL Adobe Commerce]安装之间的差异，以及这些自定义项如何在应用程序中交互。
- **分类** — 使用AI解释每个自定义项，汇总自定义项的用途，分组相关功能，识别实施模式，并提供上下文迁移建议。
- **映射和推荐** — 将每个功能映射到其[!DNL Adobe Commerce as a Cloud Service]等效功能，包括：默认功能、[!DNL App Builder]应用程序或Adobe服务。 然后，评估会推荐现代化路径，并评估复杂性、依赖性和实施工作。
- **报告** — 生成用于规划迁移执行的可导出路线图，该路线图允许您向利益相关者传达风险。 它还确定了优先事项、依赖项、技术债务和实施风险。

### 评估值

评估的价值在于您在承诺提供开发细节之前可以拥有的信心程度。 评估不是通过常规的范围设定做法来估计迁移，而是提供对实施情况的基于证据的了解。 这包括哪些自定义项易于迁移、需要重新设计以及可以完全停用。 评估会定期显示过时或未使用的功能，从而让您减少技术债务。

每个建议都包含支持性证据以及返回到底层实施的引文，这允许架构师和工程师在规划期间进行验证。 由于每项评估都遵循相同的方法，因此您可以使用一致的评分和规划框架来比较多种开发需求。

评估不仅仅是一个起点。 下游迁移工具使用评估结果来加快实施并维护与批准的迁移计划的一致性。 自定义分析成为应用程序现代化的蓝图，而数据评估通过分析数据库大小、实体清单和自定义表来限定数据迁移工作。

### 评估范围

迁移评估工具侧重于了解完整的迁移环境。 它分析自定义模块、插件、事件、API、cron作业、队列、与外部系统的集成、店面特征以及这些自定义所依赖的数据库模式。 此评估将其发现的内容映射到可用的[!DNL Adobe Commerce as a Cloud Service]功能，并确定应使用[!DNL App Builder]使功能现代化或针对SaaS架构重新设计的位置。

评估与其说是一种执行工具，不如说是一种规划工具。 它可确定应现代化的内容，估计实施的复杂性，并提供建议。 实施决策和架构验证仍是Adobe、合作伙伴和客户工程团队之间的协作活动。

由第三方扩展存储在自定义表中的数据显示为迁移注意事项。 标准数据迁移不会自动迁移此数据。 可能需要自定义[!DNL App Builder]应用程序才能支持这些方案。 有关详细信息，请参阅[数据迁移指南](#data-migration-commerce-data-migration-service)。

该评估将对店面自定义和数据迁移工作流进行分析：

- 代码和店面迁移 — 评估的应用程序分析成为Commerce开发人员MCP的蓝图
- 数据迁移 — 评估的实体清单、数据库特征分析和自定义表分析确立了Commerce数据迁移服务的范围。

您还可以随着应用程序的演变重新运行评估。 这使您的团队能够验证修正工作、衡量现代化进度，并在整个项目中不断优化迁移计划。

### 后续步骤

每个[!DNL Adobe Commerce as a Cloud Service]迁移都应该从评估开始。 这是一种在开始实施前确定范围、减少不确定性和创建共享迁移蓝图的低成本方法。

有关评估工具和下游开发人员工作流的详细信息，请参阅[Adobe Commerce开发人员MCP](https://developer.adobe.com/commerce/extensibility/developer-agent/)。

## 代码和店面迁移（Commerce开发人员MCP）

在[!DNL Adobe Commerce on Cloud]中或本地自定义可以使用进程内PHP — 在应用程序中运行的模块、插件和事件观察程序。 [!DNL Adobe Commerce as a Cloud Service]是一个无版本的SaaS平台，该模型不再适用。 自定义项作为进程外的[!DNL Adobe Developer App Builder]应用程序运行，这些应用程序通过事件和API与Commerce集成。 使存储区对此体系结构的自定义实现现代化通常是[!DNL Adobe Commerce as a Cloud Service]迁移中最重大的工程工作。

### 代码迁移概述

从迁移评估开始，Commerce开发人员MCP提供了一个对话式IDE体验，用于将旧版PHP自定义更新到[!DNL App Builder]应用程序中。 它还为Edge Delivery Services (EDS)上的店面重建提供援助。 通过直接使用迁移评估工具的调查结果，Commerce开发人员MCP通过减少手动解释、维护可跟踪性和确保整个过程的一致性，使实施与批准的迁移路线图保持一致。

虽然迁移是主要用例，但Commerce开发人员MCP被设计为[!DNL Adobe Commerce]的综合AI开发代理。 MCP支持现代化、新开发、操作工作流以及对[!DNL Adobe Commerce as a Cloud Service]的所有更新。 这种灵活性级别允许团队在迁移后很长时间继续构建和扩展Commerce应用程序。

### Commerce开发人员MCP

利用[迁移评估](#migration-assessment-tool)中的调查结果，Commerce Developer MCP通过迭代开发工作流将已识别的自定义项转换为[!DNL App Builder]个应用程序。 使用这些工具进行开发时，请考虑以下准则：

- **从Blueprint开始** - Commerce开发人员MCP使用迁移评估，使用其标识的自定义项、建议和迁移优先级作为实施计划的基础。

- **计划每个自定义** — 对于每个自定义，Commerce Developer MCP都会制定一个规范，该规范描述推荐的[!DNL Adobe Commerce as a Cloud Service]架构、所需的集成模式以及过渡到进程外应用程序所需的任何重新设计。

- **协作构建** - Commerce开发人员MCP不会最初生成代码，而是通过规划实施、讨论架构、生成和优化代码、验证建议的模式以及提供部署指导，在整个开发生命周期中为您提供帮助。 开发人员可以通过自然语言反复地优化生成的实施，使项目详细信息在整个现代化工作中共同演进。

  - 生成的实施旨在加快交付，同时让工程团队保持完全可查看、可测试和可扩展。

- **集成和部署** - Commerce开发人员MCP通过适当的集成模式将应用程序连接到Commerce，协助部署工作流，并在部署之前根据建议的架构模式验证实施，从而提高一致性并减少重复工作。

  - Commerce开发人员MCP包含[!DNL Adobe Commerce App Builder] MCP，它直接在您的开发工作流中提供域知识、实现模式、架构指导、上下文产品专业知识和经验证的编码实践。 无论开发人员是直接与Adobe开发人员MCP合作，还是与其他代理（如Claude、Cursor或Copilot）结合，这都可以确保MCP建议与Commerce的最佳实践保持一致。

### 店面现代化

在前端，Commerce开发人员MCP使用Adobe Commerce样板、放置组件和EDS块在Commerce的Edge Delivery Services (EDS)上实现[店面](https://experienceleague.adobe.com/developer/commerce/storefront/)的现代化。

Commerce开发人员MCP根据Commerce样板加载现有店面项目。 它通过以下方式使您的店面现代化：

- 生成响应EDS块
- 生成Commerce感知页面数据（主页、PLP、PDP、购物车、结账、帐户）
- 构成和扩展下拉组件
- 将设计转换为EDS实施
- 将旧式整体式店面转换为可组合的EDS块体系结构

MCP还协助：

- 组件现代化
- 可重用块组合
- 体验优化
- 与当前Edge Delivery Services最佳实践保持一致

### 开发人员MCP值

从进程中的PHP自定义移动到可组合的[!DNL App Builder]应用程序代表着体系结构上的重大转变。 Commerce开发人员MCP通过将[!DNL Adobe Commerce]知识、[!DNL App Builder]实施模式和产品最佳实践直接嵌入开发工作流来填补这一空白。

包含此上下文可提高交付速度和工程质量的一致性。 团队可以更快地实现应用程序的现代化，同时按照一致的架构指导制定实施。

通过嵌入推荐的实施模式，Commerce开发人员MCP降低了对个人专业知识的依赖，并帮助组织跨项目以一致的方式扩大现代化工作。

迁移过程也是改进现有实施的一个机会。 团队可以简化旧版自定义设置、淘汰过时的功能、采用SaaS功能以及使应用程序体系结构现代化，而不是继续承担历史性的技术债务。

由于Commerce开发人员MCP直接使用迁移评估，因此所有现代化工作都可追溯到最初的评估，确保实施与批准的迁移路线图保持一致。

Commerce开发人员MCP还通过鼓励模块化[!DNL App Builder]应用程序来促进可组合应用程序设计，这些应用程序可以随着业务需求的变化而独立地发展。

### 开发人员MCP范围

在后端，Commerce开发人员MCP通过将PHP模块、插件和事件观察程序转换为[!DNL App Builder]应用程序来使自定义和集成层现代化，并建立集成模式以将其与Adobe Commerce连接。 它还加快了结账、支付和管理UI之间的开发。

在前端，Commerce开发人员MCP [在Edge Delivery Services上使Commerce店面](#storefront-modernization)现代化。

MCP不处理数据迁移。 通过[Commerce数据迁移服务](#data-migration-commerce-data-migration-service)迁移业务数据。 当业务逻辑或自定义表需要应用程序现代化时，MCP支持所需的[!DNL App Builder]应用程序。

### 后续步骤

一旦迁移评估工具路线图确定了迁移范围和优先级，代码和店面现代化就会开始。

有关如何安装和使用MCP的更多信息，请参阅[Commerce开发人员MCP](https://developer.adobe.com/commerce/extensibility/developer-agent/)文档。

## 数据迁移（Commerce数据迁移服务）

迁移到[!DNL Adobe Commerce as a Cloud Service]可能需要迁移多年的数据，包括：目录、订单、客户和配置。

Commerce数据迁移服务将手动迁移替换为单个、可重复且自动化的过程。 它使复杂的数据库迁移更可预测、更有效。

### Commerce数据迁移服务

迁移使用引导式工作流，由Docker命令行工具(`./bin/console migration`)驱动。 系统集成商或操作员针对源存储运行此工作流。

核心数据迁移是自动化的，但大多数迁移都涉及非标准架构、扩展和边缘案例，因此所有迁移都从对源存储进行[评估](#migration-assessment-tool)开始。 在验证凭据和连接、注册迁移并建立验证基线后，您可以继续数据迁移。

迁移服务工具执行以下数据管理步骤：

1. **提取和转换** — 从源中并行提取所有相关数据并为[!DNL Adobe Commerce as a Cloud Service]重新设置其形状。 系统会过滤掉不兼容的数据，并重新映射自定义属性和其他结构。
1. **加载** — 将提取的数据传输到Commerce数据迁移服务。 该服务将数据加载到[!DNL Adobe Commerce as a Cloud Service]中，然后重新构建索引并摄取目录。
1. **验证** — 比较数据库级别的源数据和目标数据。 然后，该服务通过店面GraphQL和管理员REST API验证一个实时记录示例以验证数据。
1. **报告** — 将每个步骤的结果合并到最终迁移报告中。

这些数据移动阶段需要一个维护窗口，但在准备阶段，存储可保持正常运行，将停机时间降至最低。

### 迁移服务价值

Commerce数据迁移服务通过使用证据来保持数据完整性。 通过比较源数据和目标数据，并通过API验证实时记录样本来验证每次迁移。 提取期间会自动过滤并重新映射未完全映射到[!DNL Adobe Commerce as a Cloud Service]的数据（如自定义属性）。

迁移服务针对企业规模数据库而设计。 数据迁移是异步分区和处理的，允许可靠地迁移大型目录和大量订单历史记录。 随着管道的增长，多个迁移可以并行运行。 如果迁移中断，则从上一个已完成的阶段继续，并自动检测和重试停止的作业。

可通过以下方式将停机时间降至最低：

- 大部分工作会在存储保持活动状态时执行，这意味着只有最终转换需要维护时段。
- 数据迁移使用高效的直接SQL读取和写入，并跳过不需要迁移的表和记录。

由于迁移涉及通过Adobe基础架构移动生产数据，因此整个路径是安全的：

- 在到达目标之前，将扫描所有上传中的恶意软件
- 引入层验证文件类型并阻止不安全的数据库操作
- 每个请求都使用Adobe IMS和网关签名验证进行身份验证

Commerce数据迁移服务在全球范围内处于生产状态，并且已经提供了多个企业级迁移。

### 自定义数据和第三方数据

迁移服务仅支持第一方核心商务数据。 迁移服务不处理自定义的第三方实体。

第三方数据可以按案例迁移，这要求对Docker提取工具进行相应的自定义。 创建自定义工具后，可以从源中提取数据并将其写入[!DNL App Builder]或第三方数据库。

由于每个扩展对其数据的建模方式不同，因此只能在确定源和目标存储的架构和位置之后设计第三方数据的迁移路径。 应尽早确定第三方数据迁移，以便有时间确定范围。

### 后续步骤

准备迁移时，请完成[数据迁移范围调查表](../assets/data-migration-scoping-questionnaire.xlsx)，该调查表需要源拓扑、实体范围、卷、合规性约束、直接转换机制以及规划迁移所需的任何[自定义表](#custom-and-third-party-data)。 完成此调查表可让Adobe评估您的环境并规划迁移时段。

查看[批量数据迁移工具指南](bulk-data/migration-tool.md)文档，了解有关工作流、支持的数据和验证的更多信息。

准备源环境的系统集成商还可以使用标准[Adobe Commerce Cloud CLI](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/dev-tools/cloud-cli/cloud-cli-overview)和[Adobe Developer Console](https://developer.adobe.com)作为IMS凭据。
