---
title: 目录概述
description: 了解如何定义渠道和策略。
hide: true
recommendations: noCatalog
source-git-commit: d716dd9d75beb642bfad30271b6ecd3490ee7328
workflow-type: tm+mt
source-wordcount: '1604'
ht-degree: 0%

---

# 目录概述

>[!NOTE]
>
>本文档描述了早期访问开发中的产品，并未反映用于正式发布的所有功能。

产品目录对于在线购物体验至关重要，它使客户能够浏览、搜索和进行购买。 为了提高运营效率，产品目录应密切反映公司的业务结构。 企业通常需要根据地理市场、分销渠道、客户细分和其他变量以不同的价格销售产品。 为了适应这种情况，电子商务平台必须提供灵活的目录数据模型，允许公司生成针对这些方案定制的目录变体。 Adobe通过提供由渠道和策略提供支持的促销服务来满足这些需求。 Merchandising Services提供了构建块，商家可以使用它来大规模创建和管理目录。 这使企业能够配置与其业务结构和走向市场战略相一致的目录。

从较高层面来看，借助促销服务，您可以：

- 使用单个基础目录满足您的所有业务需求。 在新的品牌、市场、业务单元、走向市场渠道和客户细分中快速扩展您的目录，而无需完全的重新架构。 这消除了数据重复，并设置了电子商务平台以实现高运营效率。
- 通过设计产品目录以反映您的业务（包括产品、客户、定价和分发），解锁目录联合并提供正确的内容。
- 快速摄取和更新目录数据，并快速将更新交付到店面，以满足您的促销活动和营销活动需求。
- 通过由Edge Delivery Services提供支持的、随时可用、速度快的UI组件实现完美的Lighthouse分数，以实现无缝的产品浏览和推荐。
- 采用Adobe可扩展性架构([App Builder](https://experienceleague.adobe.com/zh-hans/playlists/commerce-get-started-app-builder-development))的现代可组合架构，以使用Adobe的[API Mesh](https://experienceleague.adobe.com/zh-hans/playlists/commerce-get-started-app-builder-and-api-mesh)导入产品数据并增强Headless商务店面。

>[!INFO]
>
>要了解渠道和策略支持的促销服务中可用的API，请参阅[开发人员文档](https://developer-stage.adobe.com/commerce/services/composable-catalog)。

## 架构

由渠道和策略提供支持的促销服务是一种高度可扩展、灵活的目录数据模型，可轻松解锁多品牌、多业务单元、多语言用例。 此模型将传统Adobe Commerce产品范围（网站、商店、商店审查）的使用替换为新的Merchandising Services产品范围（渠道、策略和区域设置）。

下图提供了有关促销框架的简要视图。

![[!DNL Merchandising Services]架构](../assets/merchandising-svcs-architecture.png)

在此图的顶部，目录数据（PIM、ERP等）被引入到Merchandising Services框架中。 此目录数据包含SKU。 每个SKU都包含范围详细信息（区域设置）和产品属性，这些属性映射到新的Merchandising Services产品范围（渠道、策略和区域设置）。

当所有这些数据都引入到“促销”框架中时，结果是在目录服务数据管道中可用的新统一基础目录。 在图表的下一部分，您会看到多个渠道。 每个渠道表示一个业务单元。 例如，*Texas retail*、*Texas retail seagural*&#x200B;等。 如图所示，您可以跨渠道共享区域设置、策略和价格手册&#x200B;。

最后，该图显示了如何在不同位置(例如Edge Delivery Services店面、市场、广告频道、自定义微型店面等)呈现这些独特的目录数据。

要了解如何使用目录数据摄取API将目录数据摄取到促销，以及如何使用目录管理和规则API设置区域设置、策略和价格手册，请参阅[开发人员文档](https://developer-stage.adobe.com/commerce/services/composable-catalog/)。

要详细了解构成促销服务的概念，请参阅以下部分。

## 产品目录管理

产品目录管理包括两个不同的方面：产品数据和产品上下文。 促销服务尊重这些职责的分离，并为每个职责提供独立管理。

- **产品数据** — 正在销售什么产品，以什么价格销售？
- **产品上下文** — 谁向谁销售产品以及在何处销售？

![[!DNL Merchandising Services]方面](../assets/merchandising-svcs-parts.png)

### 产品数据

产品数据包括以下类型：

- **产品** — 代表实物商品或无形服务的个别SKU或SKU集合，其属性代表产品，包括说明、重量、大小、尺寸等。 属性还为SKU指定渠道和策略范围。 产品可以分组为各种产品类型，如简单、可配置、捆绑、捆绑包、订阅等。
- **元数据** — 产品属性元数据定义和管理产品属性在产品列表、详细信息页面、搜索结果等店面中的显示方式。 元数据还定义了如何在搜索中使用产品属性 — 排序、筛选、搜索权重等。
- **定价书籍和价格** — 确定产品的售价。 在促销服务中，产品SKU和价格是相互分离的，因此您能够为单个SKU定义多个价格手册。 通过使价格与SKU脱钩，您可以解锁不同客户层、业务单位和地理区域内的特定价格。 您可以定义常规价格和折扣价格，并大规模管理所有这些价格。
- **Assets** — 与产品关联的工件，如图像、视频、PDF或其他文件类型（未来路线图）。

### 产品上下文管理

产品上下文管理包括以下方面：

- **渠道** — 分销渠道定义企业销售产品的路径。 渠道是封装区域设置和策略的最高级抽象。
   - 示例：汽车业经销商。 为多品牌企业集团设立附属公司。 供应商的制造地点。
- **策略** — 数据访问筛选器，允许您向正确的目标提供正确的内容。 此概念支持目录联合功能。
   - 示例：销售点实体商店、市场、广告管道(Google、Facebook、Instagram)
- **作用域** — 表示目录的语言（区域设置），例如`en-US`。 在目录数据摄取期间在SKU级别设置范围。

在产品数据摄取和更新期间，SKU包含范围和属性的详细信息（属性映射到渠道和策略）。 它们定义SKU所属的产品上下文标识符：

![[!DNL Merchandising Services]产品上下文标识符](../assets/merchandising-svcs-product-id.png)

在上图中，每个SKU都提供：

- 范围标识符&#x200B;
   - 区域设置：必&#x200B;填
- 产品属性
   - 产品属性用于映射到相关渠道和策略&#x200B;。
   - 示例：作为汽车制造商，您可以选择为产品属性创建渠道和策略组合： (1)经销商(2)汽车品牌&#x200B;。
- 价格和分配的价格手册
   - 每个SKU可以使用多个价格手册定义多个价格。
   - 示例：您向员工提供汽车部件的较低常规价格，额外折扣25%。 您为VIP客户提供更优惠的固定价格（10%的折扣）。 产品SKU价格信息可确保为每个客户细分显示正确的价格。

渠道和策略定义是使用专用API创建的：

![[!DNL Merchandising Services]通道、策略和范围映射](../assets/merchandising-svcs-scope-map.png)

- **范围**（区域设置） — 在产品数据引入期间在SKU级别设置。&#x200B;
- **渠道** — 使用专用API创建的定义。&#x200B;AEM
- **策略** — 使用专用API创建的定义。

## 主要功能

| 主要功能 | 收益 |
|---|---|
| **将目录数据直接摄取到storefront services管道**：将目录数据直接摄取到storefront浏览和搜索生命周期（产品显示页面、产品列表页面、搜索结果页面等）的目录服务管道。 | <ul><li>直接将目录数据摄取到Storefront Service管道，该管道为以下产品提供支持：目录服务、产品发现（实时搜索）和产品推荐。 这样，您就可以大规模地为数百万个SKU提供目录更新。 这解锁了时效性强的大规模促销管理。 </li></ul> |
| **新目录产品范围**：渠道、策略和范围是促销服务引入的新产品范围。 这些产品范围将替换店面服务层中的网站、商店和商店审核范围。 [了解详情](#product-context-management)。 | <ul><li>借助新的范围，Merchandising Services释放了使用单个基础目录轻松扩展到多地理位置、多业务单元、多品牌和多语言用例的能力。</li><li>消除目录管理中的数据冗余。</li></ul> |
| **扩展到数千万SKU** | 大规模解锁目录管理。 在这里，您可以轻松摄取和管理200MM以上的SKU。 |
| **产品类型支持** | <ul><li>简单、可配置</li><li>捆绑包和捆绑包（未来路线图）</li><li>订阅和计划（未来路线图）</li></ul> |
| **Headless商务** | <ul><li>通过目录服务、产品发现（实时搜索）和产品推荐API，完全支持Headless商务实施。</li></ul> |
| **现代闪电般快速的UI组件** | <ul><li>开箱即用的UI组件支持产品搜索和产品推荐。</li><li>UI组件是可扩展和灵活的，因此Adobe的Edge Delivery服务以及任何其他店面实施都可以使用这些组件。</li></ul> |

## 哪种类型的商家从促销服务中受益最大？

下表重点说明了商家面临的常见挑战，以及渠道和策略支持的促销服务如何解决这些挑战。

| 商家类型 | 用例 | 已解决的问题 |
|---|---|---|
| 多品牌企业集团 | <ul><li>他们卖好几个品牌</li><li>他们在多个国家销售</li><li>他们用不同的语言销售</li></ul> | 使用单个基本统一目录并实现运营效率，同时扩展到多个品牌、地区和语言。 |
| 汽车/制造部件联合体 | <ul><li>销售汽车或机器零部件。 所有客户可以使用相同的产品。</li><li>不同的经销商向客户出售零件</li><li>每个交易商都有自己的价格、库存和运输方式</li></ul> | 要有不同的运输集成，每个经销商应有一个单独的网站。 但是，单独的网站会强制使用典型的目录数据模型复制数据。 所以，如果在美国有3000个经销商，一个商家创造了3000个目录副本，即使相同的目录被所有的经销商使用。 这种重复数据消除会干扰性能限制。 促销服务消除了数据重复。 |
| 包装/物流公司 | <ul><li>它们有几个运输地点</li><li>每个客户的价格各不相同</li><li>在2个地点为2个客户提供的相同产品有4个可能的价格</li></ul> | 尽管使用客户组涵盖每个客户的定价，但典型的目录数据模型无法管理每个位置的价格。 此外，商家希望每个位置/网站具有唯一的可见性规则。 可以通过Merchandising Services大规模解锁此类复杂价格和可见性规则的管理。 |

<!--### Where to go from here

- Ingest data into Merchandising Services using the [data ingestion API](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/using-the-api/).
- Manage your catalog and define the channels, policies, and scopes using the [catalog management API](https://developer-stage.adobe.com/commerce/services/composable-catalog/admin/using-the-api/)
- [Complete a tutorial](https://developer-stage.adobe.com/commerce/services/composable-catalog/merchandising-services-use-case/) that shows how a company with a single base catalog can use the Merchandising Services APIs to add product data, define catalogs using projections, and retrieve the catalog data for display in a headless storefront.-->
