---
title: '[!DNL Catalog Service]'
description: 通过 [!DNL Catalog Service] (一种高性能GraphQL API，可减少产品页面、类别页面和搜索结果的页面加载时间)加速Adobe Commerce店面。
role: Admin, Developer
recommendations: noCatalog
exl-id: 525e3ff0-efa6-48c7-9111-d0b00f42957a
source-git-commit: e582bff6ee8ee7c4213f04bdab984efa94333fb6
workflow-type: tm+mt
source-wordcount: '1323'
ht-degree: 0%

---

# Adobe Commerce的[!DNL Catalog Service]

适用于Adobe Commerce扩展的[!DNL Catalog Service]通过专用的GraphQL API提供优化的只读目录数据，从而缩短店面加载时间。 此服务专门用于增强与产品相关的页面体验，从而加快页面加载并提高转化率。

[!DNL Catalog Service]提供的丰富视图模型数据包括产品详细信息、属性、库存和价格，支持快速呈现与产品相关的店面体验，例如：

- 产品详细信息页面
- 产品列表和类别页面
- 搜索结果页面
- 产品轮播
- 产品比较页面
- 渲染产品数据的任何其他页面，如购物车、订单和愿望清单页面


## 主要优势和功能

- **页面加载速度更快**：优化查询，目录数据检索速度比核心GraphQL系统快10倍
- **转化率提高**：加载时间越短，用户体验越好
- **简化的产品类型**：基于简单和复杂产品类型的统一架构降低了开发人员的复杂性
- **增强的价格精确度**：支持包含4位小数的16位值
- **分离的架构**：目录数据的独立GraphQL系统可确保高性能，而不会影响Commerce的核心操作
- **实时数据同步**：目录服务通过SaaS数据导出扩展与Adobe Commerce应用程序保持同步，确保查询返回最新的目录数据
- **数据管理功能板**：从Adobe Commerce管理界面监视和管理数据同步操作
- **API Mesh集成**：选择性地与Adobe Developer App Builder的[API Mesh集成](https://developer.adobe.com/graphql-mesh-gateway/)，以将Adobe Commerce GraphQL系统与其他内部和第三方API相结合，以扩展Catalog Service GraphQL架构并添加自定义数据或功能


## 架构概述

[!DNL Catalog Service]使用[GraphQL](https://graphql.org/)请求和接收目录数据，包括产品、产品属性、库存和价格。 GraphQL是一种查询语言，前端客户端使用它与在后端(如Adobe Commerce)上定义的应用程序编程接口(API)进行通信。 GraphQL是一种常用的通信方法，因为它非常轻量，允许系统集成商指定每个响应的内容和顺序。

Adobe Commerce提供两种用途不同的GraphQL系统：

### 核心GraphQL System

- **用途**：适用于所有Commerce操作的全功能API
- **功能**：针对产品、客户、购物车、结账等的查询（读取）和变动（写入）
- **限制**：产品查询未针对速度进行优化
- **用例**：一般Commerce操作和写入操作

### 目录服务GraphQL System

- **用途**：仅高性能产品目录查询
- **功能**：产品、属性、库存和价格的只读查询
- **优势**：比产品数据的核心系统快很多
- **用例**：速度至关重要的店面产品体验

目录服务可用的数据由SaaS数据导出扩展提供。 此扩展在Commerce应用程序与连接的Commerce服务之间同步数据，以确保对服务GraphQL API端点的查询返回最新的目录数据。 有关管理和排查SaaS数据导出操作问题的信息，请参阅[SaaS Data Export Guide](../data-export/overview.md)。

[!DNL Catalog Service]客户可以使用[SaaS价格索引器](../price-index/price-indexing.md)，这提供了更快的价格更新和同步时间。

## 架构详细信息

下图说明了核心GraphQL系统和目录服务GraphQL系统之间的体系结构差异，说明了它们如何协作来优化店面性能：

![目录体系结构图](assets/catalog-service-architecture.png)

### 系统如何工作

**核心GraphQL系统（传统方法）：**
渐进式Web应用程序(PWA)将请求直接发送到Commerce应用程序，后者在返回响应之前通过多个子系统处理每个请求。 这种多步往返可能会导致页面加载时间变慢，从而潜在地降低转化率。

**目录服务（优化方法）：**
目录服务充当一个Storefront Services Gateway，可访问专用的优化数据库，该数据库包含产品详细信息、属性、变体、价格和类别。 该服务通过自动索引来维护与Adobe Commerce的同步，从而绕过传统的请求 — 响应周期来显着减少延迟。

GraphQL的核心系统和服务不会直接相互通信。 您可以从不同的URL访问每个系统，并且调用需要不同的标头信息。 这两个GraphQL系统旨在共同使用。 [!DNL Catalog Service] GraphQL系统增强了核心系统，使产品店面体验更快。

您可以选择实施适用于Adobe Developer App Builder[的](https://developer.adobe.com/graphql-mesh-gateway/)API Mesh，以便使用Adobe Developer将两个Adobe Commerce GraphQL系统与私有和第三方API以及其他软件接口集成。 可以配置网格以确保路由到每个端点的调用在标头中包含正确的授权信息。

## 体系结构详细信息

以下部分介绍了这两种GraphQL系统之间的一些差异。

### 架构管理

由于目录服务作为一种服务运行，因此集成商无需担心Commerce的基础版本。 所有版本的查询语法相同。 此外，该架构对于所有商家都是一致的。 这种一致性使得建立最佳实践更加容易，并显着提高了店面构件的重复使用率。

### 产品类型的简化

架构将产品类型的多样性减少为两个用例：

- **简单产品** — 目录服务将Adobe Commerce简单、虚拟、可下载和礼品卡产品类型映射到`simpleProductViews`。 此类型具有：
   - 单一、固定的价格和数量
   - 常规价格（折扣前）和最终价格（折扣后）
   - 支持产品属性，如颜色、大小和其他特征

- **复杂产品** — 目录服务将Adobe Commerce可配置、捆绑包和分组产品类型映射到`complexProductViews`。 复杂产品是多个简单产品的集合，这些产品可以配置或捆绑在一起。
   - 每个部件简单产品可以有自己的价格。
   - 购物者可以指定单个组件产品的数量。
   - 产品选项（如大小、颜色、材质）是统一的，无论产品类型如何，均以相同的方式工作。 每个选项选择都指向一个特定的简单产品，该产品具有自己的属性和价格。 在购物者选择所有必需选项之前，最终产品将保持未定义状态。

#### 产品视图属性

简单和复杂的产品都有客户定义的属性，这些属性可显示在店面上。 这些属性作为[ProductViewAttributes](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/#productviewattribute-type)返回。 在Adobe Commerce中，可用的属性在创建产品时定义。 您可以从Adobe Commerce后端或以编程方式添加其他属性。 请参阅[扩展和自定义SaaS数据导出馈送数据](../data-export/extensibility-and-customizations.md)。

>[!TIP]
>
>您可以将[API Mesh与目录服务](mesh.md)一起使用，扩展目录服务GraphQL架构以添加数据或配置现有目录数据来启用新功能，而不是将数据类型添加到Commerce后端。

### 价格

简单产品表示具有价格的基本销售单位。 [!DNL Catalog Service]计算折扣前的常规价格以及折扣后的最终价格。 定价计算可以包括固定产品税。 它们不包括个性化促销。

复杂的产品没有确定的价格。 相反，目录服务会返回链接的单点的价格。 例如，商家最初可以为可配置产品的所有变体分配相同的价格。 如果某些尺寸或颜色不受欢迎，商家可以降低这些变体的价格。 因此，复杂（可配置）产品的价格首先显示一个价格范围，同时反映标准和不受欢迎的变体的价格。 购物者为所有可用选项选择了一个值后，店面会显示一个价格。

目录服务支持大值（最多16位）和高小数精度（最多4位小数）的价格，从而确保准确的价格更新和计算。

>[!NOTE]
>
> 拥有[!DNL Catalog Service]的Commerce客户可以使用[SaaS价格索引器](../price-index/price-indexing.md)利用其网站上更快的价格更改更新和同步时间。

## 实现

实施过程涉及：

1. [!BADGE 仅限PaaS]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于云项目(Adobe管理的PaaS基础架构)和内部部署项目上的Adobe Commerce 。"} **[安装和配置目录服务](installation.md)** — 安装和配置目录服务扩展并使用[!DNL Commerce Services Connector]设置SaaS连接。
2. **更新店面代码**：将目录服务GraphQL查询集成到您的店面。
3. **路由查询**：所有目录服务查询都通过GraphQL网关（载入期间提供的URL）
4. **监视数据同步并排除其故障**：验证改进的性能并监视结果


