---
title: 将 [!DNL Adobe Commerce] 与 [!DNL Adobe LLM Optimizer]集成
description: 连接 [!DNL Adobe Commerce] 到 [!DNL Adobe LLM Optimizer] 以监视LLM中的目录信号并部署批准的目录优化。
role: Admin, User, Leader
recommendations: noCatalog
badgePaas: label="仅限PaaS" type="Informative" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于云项目（Adobe管理的PaaS基础架构）和内部部署项目上的Adobe Commerce 。"
source-git-commit: 47348a44ff7c5f890c10594f44cae6e771be046f
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 0%

---

# 将[!DNL Adobe Commerce]与[!DNL Adobe LLM Optimizer]集成

>[!IMPORTANT]
>
>对此集成的访问受限。 请联系您的技术客户经理以了解详细信息。

[!DNL Adobe LLM Optimizer]是一个企业解决方案，可帮助品牌监控、分析和优化其内容在大型语言模型(LLM)和AI助理的答案中的显示方式。 随着购物者越来越多地使用AI工具进行研究和产品发现，LLM Optimizer有助于确保您的品牌和目录被准确引用并在上下文中浮现。

本指南介绍当您的产品目录存储在Commerce中时，**[!DNL Adobe Commerce]**&#x200B;如何适应该工作流。 您将了解哪些功能可用，需要哪些配置，以及部署的优化在管理员中和各摄取渠道中的行为方式。

>[!NOTE]
>
>[!DNL Adobe LLM Optimizer]是一个独立的Adobe解决方案。 核心监控和机会工作流不需要[!DNL Adobe Experience Manager] (AEM)或其他Adobe应用程序。 仅当您的目录连接到Commerce并且您选择将批准的更改推送到[!DNL Adobe Commerce]中时，才会应用特定于LLM Optimizer的部署操作。

## 集成支持的功能 {#what-integration-enables}

通过将LLM Optimizer连接到您的[!DNL Adobe Commerce]目录，您可以从广泛的内容见解转变为&#x200B;**可识别目录的**&#x200B;推荐：

- **确定目录数据（如标题、说明和结构化信号）中的**&#x200B;差距和不一致，这些会影响LLM解释产品的方式。
- **评论**&#x200B;建议改进支持上下文，包括理由和前后比较。
- **直接将**&#x200B;选定的优化（如产品名称和说明更新）部署到Commerce目录，以确保管理工作流程、网格和店面数据保持一致。

当目录源为[!DNL Adobe Commerce]时，Adobe可以支持完整的端到端工作流：自动识别机会、建议更改和应用批准的修复。 对于源自Commerce外部的目录，LLM Optimizer仍可以分析和建议改进功能，但应用更改取决于您的集成模型（例如，镜像目录或手动更新）。 请参阅[集成限制和边界](boundaries-limits.md)。

## 这是给谁的 {#who-this-is-for}

- **希望产品数据在LLM驱动的答案中准确且一致，并且需要控制方式大规模改进目录复制的数字营销人员和推销员**。
- **Commerce管理员**，他们拥有提供产品属性的目录完整性、管理流程和集成(API、CSV、PIM)。

## 先决条件 {#prerequisites}

当您&#x200B;**访问** Adobe Commerce与Adobe LLM Optimizer的集成时，以下先决条件适用。 请联系您的技术客户经理以了解详细信息。

- 您的店面可以由面向LLM和代理的机器人抓取，其中此抓取功能是LLM Optimizer衡量和优化策略的一部分（目录感知洞察的一般先决条件）。
- 对于Commerce支持的部署工作流，所需的Commerce服务和目录连接已启用且运行正常。 [将Adobe Commerce连接到LLM Optimizer](get-started/connect-to-llmo.md)中介绍了任务级设置。

您还应了解数据如何在系统之间移动：

### 高级数据流 {#high-level-data-flow}

从概念上讲，目录优化遵循两种模式（您的项目可能使用一种模式或同时使用两种模式，具体取决于功能）：

| 方向 | 用途 |
| --- | --- |
| **Commerce目录 — > LLM Optimizer** | 目录和URL信号为LLM Optimizer UI中的商机和建议提供信息。 |
| **LLM Optimizer -> Commerce** | 在您批准部署操作后，产品名称和描述的更新将写入主Commerce目录，以便管理员和店面都能反映优化后的值。 |

### [!DNL Adobe Commerce]与第三方目录进行比较 {#commerce-vs-third-party}

| 目录源 | 典型的LLM Optimizer覆盖范围 |
| --- | --- |
| **[!DNL Adobe Commerce]** | 强烈支持标识和建议，以及部署您配置的已批准目录字段更新。 |
| **第三方商务** | 支持标识和建议；在商家系统中自动部署取决于导出、镜像或合作伙伴工作流，而不是直接写入商家的源目录。 |

## 目录代理、Storefront MCP和LLM Optimizer {#catalog-agent-and-mcp}

您的[!DNL Adobe Commerce] **产品目录**&#x200B;是产品数据的记录系统：名称、描述、属性、定价和库存。 为了支持AI辅助的发现和优化，**Adobe Commerce Storefront MCP**（模型上下文协议）是您的实时Commerce目录数据与Adobe AI体验之间的结构化接口。

**目录代理**&#x200B;位于Storefront MCP顶部。 目录代理允许[!DNL Adobe LLM Optimizer]通过找出差距、提出改进建议并在您批准它们时部署更改，来查询、扩充目录和PDP上下文并对其执行操作。 这些功能显示在[将LLM Optimizer与Adobe Commerce结合使用](get-started/use-llmo-with-commerce.md)中描述的LLM Optimizer工作流中。

## 目录代理如何改进适用于LLM的Commerce {#catalog-agent-optimizations}

目录代理通过两个互补优化来解决可发现性问题：产品详细信息页面扩充和产品目录扩充。

### 产品详细信息页面扩充 {#pdp-enrichment-overview}

**产品详细信息页面(PDP)扩充**&#x200B;建议对产品页面内容进行细化，这样当购物者通过AI助手和类似工具发现产品时，您的商品就会更清晰地阅读。 目标是提高清晰度和一致性，同时不更改您的团队已推销的店面布局。 您可以在LLM Optimizer中查看建议，并在准备就绪后进行部署。

部署后，点按实时产品页面以确认购物体验仍符合您的预期。

### 产品目录扩充 {#catalog-enrichment-overview}

**产品目录扩充**&#x200B;建议更清晰的&#x200B;**产品名称**&#x200B;和&#x200B;**产品描述**，其中副本较细、模糊或不一致。 每个建议都包含上下文，以便您的团队可以决定要更改的内容。 当您批准更新时，该更新可以应用于您的[!DNL Adobe Commerce]目录，以便管理员、店面和使用这些字段的其他体验反映相同的措辞。

由于这些字段位于Commerce中，因此改进一次名称或描述可以使读取该产品数据的每个渠道受益（具体取决于系统刷新的方式和时间）。

## 相关主题 {#related-topics}

- [将Adobe Commerce连接到LLM Optimizer](get-started/connect-to-llmo.md)
- [将LLM Optimizer与Adobe Commerce一起使用](get-started/use-llmo-with-commerce.md)
- [集成限制和边界](boundaries-limits.md)
