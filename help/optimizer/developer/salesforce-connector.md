---
title: Salesforce Commerce Connector
description: 了解 [!DNL Commerce Optimizer SFCC Connector] ，它提供了一个起点，用于将Salesforce Commerce B2C与 [!DNL Adobe Commerce Optimizer] 集成以同步目录数据并实施和自定义连接器来支持业务操作。
role: Admin, Developer
source-git-commit: c6725fc524e9d239ccc0f16701e92ad5d2fc7729
workflow-type: tm+mt
source-wordcount: '1115'
ht-degree: 0%

---

# 适用于Adobe Commerce Optimizer的Salesforce Commerce Connector

[!DNL Commerce Optimizer Salesforce Commerce Connector]构建于Adobe App Builder技术之上，支持将目录数据从Salesforce Commerce Cloud B2C无缝传输和管理[!DNL Adobe Commerce Optimizer]。 它连接了两个平台，使产品信息、定价和更新保持同步，而无需重新调整平台。

该连接器开箱即用地提供可靠的数据同步功能，并灵活地自定义工作流程以满足您的业务需求。

有关端到端视频教程系列，请参阅[了解Salesforce Commerce云入门工具包](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-commerce-optimizer/sfcc-starter-kit/overview)。

## 主要功能

* **目录数据同步：**&#x200B;将产品数据（包括变型、价格手册和结构）从Salesforce Commerce B2C推送到Adobe Commerce Optimizer中，以保持店面和体验驱动型应用程序处于最新状态。
* **价格同步：**&#x200B;直接从Salesforce Commerce B2C导入和管理价格数据。
* **支持多种数据类型：**&#x200B;同步产品、定价和目录结构，以反映复杂的促销配置。

* **灵活同步工作流**
   * **计划的同步：**&#x200B;使用cron作业计划自动进行更新，无需手动操作。
   * **按需更新：**&#x200B;即时触发SKU级别的更新，以进行紧急更改、更正或产品发布。

* **为可扩展性构建**
   * 使用自定义[Salesforce Commerce B2C API](https://developer.salesforce.com/docs/commerce/commerce-api/guide/get-started.html) (SCAPI)端点以实现兼容性并轻松适应独特或高级用例。
   * 通过目录和价格同步随业务启动进行扩展，然后扩展工作流以支持其他集成或业务逻辑。
   * 在不重建核心集成的情况下配置和改进工作流。

>[!NOTE]
>
>该连接器专为Salesforce Commerce Cloud B2C设计。 它不支持基于不同技术栈栈构建的Salesforce B2B或D2C产品。

## 谁将从Salesforce Connector中受益？

[!DNL Salesforce Commerce Connector]适用于：

* **现有Salesforce Commerce Cloud B2C客户**&#x200B;增强店面功能
* **需要跨多个店面进行高级推销和个性化功能的多品牌组织**
* **寻求通过Adobe的Edge Delivery Services改进性能的企业**，以获得更快的店面体验
* **具有复杂定价结构的公司**&#x200B;同步了复杂的价格手册和特定于区域设置的定价
* **AEM客户**&#x200B;在将Salesforce Commerce B2C店面与Edge Delivery Services结合使用时，从Adobe Commerce管理产品目录
* **具有多区域设置要求的零售商**&#x200B;正在同步不同市场和语言的本地化产品信息

## 用例

该连接器支持几个主要用例：

### 目录数据摄取和店面显示

此主要用例演示了从Salesforce Commerce B2C到Adobe Commerce店面的完整数据流：

1. **初始目录摄取：**&#x200B;批量加载您的整个Salesforce Commerce目录，包括带有变体、价格手册和定价信息的简单产品。
1. **自动增量更新：**&#x200B;自动将产品更新从Salesforce Commerce目录管理UI同步到[!DNL Commerce Optimizer]。
1. **店面集成：**&#x200B;使用[!DNL Commerce Optimizer]店面API在您的Adobe Commerce Edge Delivery服务店面中显示同步的目录数据。
1. **实时更新：**&#x200B;在Salesforce中进行更改后，立即在店面上查看更新的产品信息（名称、价格、描述）。

### 多区域设置产品管理

利用Salesforce Commerce B2C本地化功能：

* 针对不同的区域设置，同步Salesforce Commerce B2C中的本地化版本产品文本字段（名称、描述）。
* 将Salesforce区域设置概念1:1映射到[!DNL Commerce Optimizer]区域设置。
* 针对不同的本地化支持多个产品摄取周期。
* 保持全球产品目录的一致性。

## 架构和组件

[!DNL SFCC Connector]在Salesforce Commerce B2C实例和[!DNL Commerce Optimizer]之间提供了一个可靠的集成层。 连接器通过一系列同步操作来操作，这些同步操作用于传输目录数据、价格手册和产品信息。

1. **数据提取** — 对您的Salesforce Commerce B2C实例进行身份验证，并使用自定义SCAPI提取目录数据。
1. **数据转换** — 转换产品数据以匹配[!DNL Commerce Optimizer]数据模型和架构要求。
1. **数据摄取** — 使用ACO TypeScript SDK将转换后的数据安全地传输到[!DNL Commerce Optimizer]。
1. **店面集成** — 同步数据通过[!DNL Commerce Optimizer]个API可用于店面体验。

下图说明了集成的高级数据流：

![Salesforce Commerce连接器架构](../assets/sfcc_starter_kit.png){zoomable="yes"}

### 关键组件

[!DNL Commerce Optimizer SFCC Connector]包含几个关键组件：

* **ACO SFCC Starter Kit App Builder应用程序** — 提供无服务器功能，用于处理SFCC和Adobe Commerce Optimizer之间的数据同步。
* **自定义SFCC墨盒** — 使用数据提取所需的API扩展Salesforce Commerce Cloud实例的所需墨盒。
* **管理UI** — 用于监视同步状态和管理连接器操作的Web界面。

### 同步过程

连接器支持多种同步模式。

| 同步模式 | 描述 |
|-----------|-------------|
| **完全站点同步** | 全面同步您配置的Salesforce Commerce Cloud网站和区域设置的所有产品、价格手册和价格。 这包括 <ul><li>产品元数据和属性</li><li>目录结构和类别</li><li>价格手册</li><li>定价信息</li><li>多区域设置产品数据</li></ul> |
| **增量同步** | 仅检索和同步自上次同步以来在Salesforce产品和价格数据中进行的更改，以确保高效且及时的更新。<br>增量同步按计划自动运行（默认值：每小时）以保持数据新鲜度。 |
| **目标同步选项** | 提供粒度同步功能： <ul><li>**价格手册同步**&#x200B;仅同步价格手册信息</li><li>**元数据同步**&#x200B;更新产品元数据和属性定义</li><li>**特定产品同步**&#x200B;按SKU同步各个产品</li></ul> |

## 重要注意事项

在规划实施时，请考虑以下关键因素：

### 数据映射和属性

* **可搜索属性：** Salesforce Commerce B2C通过UI设置可搜索属性，而API不会公开这些属性。 使用[[!DNL Catalog Data Ingestion metadata APIs]](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/#metadata)在Adobe Commerce Optimizer中手动配置这些可搜索属性。
* **属性映射：**&#x200B;根据您的业务要求，规划Salesforce Commerce B2C产品属性到[!DNL Commerce Optimizer]元数据的映射。
* **默认可搜索字段：**&#x200B;连接器自动使核心属性(`name`、`description`、`ID`)默认可搜索。

### 同步范围

* **站点选择：** Salesforce Commerce B2C具有目录附加到的站点的概念。 在完全同步期间，选择要同步的Salesforce站点。
* **区域设置管理：**&#x200B;每个Salesforce Commerce区域设置在[!DNL Commerce Optimizer]中导致单独的产品摄取周期。
* **数据卷：**&#x200B;规划实施时考虑目录大小和同步频率。

## 监控和管理

安装和配置后，[!DNL Commerce Optimizer SFCC Connector]即可从[!DNL SFCC to ACO Sync Panel]提供全面的监视和管理功能：

![Salesforce Commerce Connector管理UI](../assets/sfcc_management_ui.png){width="700" zoomable="yes"}

在将[!DNL Commerce Optimizer SFCC Connector Starter Kit]部署到App Builder项目后提供了此接口的URL。

主要功能包括：

* **同步状态跟踪：**&#x200B;监视所有同步操作的状态和时间戳。
* **连接验证：**&#x200B;测试与Salesforce Commerce Cloud和Adobe Commerce Optimizer的连接。
* **产品数据验证：**&#x200B;验证已同步的产品数据是否正确显示在店面中。
* **错误日志记录和故障排除：**&#x200B;可通过App Builder CLI访问用于故障排除的错误日志。
* **状态管理：**&#x200B;跟踪同步进度并防止与内置状态管理冲突。

## Source代码和开发资源

[!DNL Commerce Optimizer SFCC Connector]是开源的，可以自定义。 关键存储库包括：

* **[ACO SFCC Starter Kit](https://github.com/adobe-commerce/aco-sfcc-starter-kit)** — 主连接器应用程序和文档。
* **[ACO SFCC墨盒](https://github.com/adobe-commerce/aco-sfcc-cartridges)** - API集成所需的SFCC墨盒。
* **[ACO TypeScript SDK](https://github.com/adobe-commerce/aco-ts-sdk)** — 用于Adobe Commerce Optimizer的SDK集成。

这些存储库提供了用于实施和自定义连接器的完整源代码、详细文档和示例。

## 后续步骤

准备好将您的Salesforce Commerce Cloud数据与Adobe Commerce Optimizer集成了吗？ 首先查看[ACO SFCC Starter Kit存储库](https://github.com/adobe-commerce/aco-sfcc-starter-kit)中的详细实施指南，并确保您具备必要的先决条件。
