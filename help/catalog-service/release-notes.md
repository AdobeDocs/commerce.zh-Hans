---
title: '[!DNL Commerce Storefront Catalog Service Release Notes]'
description: Adobe Commerce的 [!DNL Catalog Service] 的最新发行信息。
feature: Services, Catalog Service, Release Notes
exl-id: 74f2e46a-5592-4857-a6d7-b95b85d8b4cc
TQID: https://experienceleague.adobe.com/-yxW4sTuk7LPjGy5YsQ65phtkBLiByg8SmBaQPHMevM
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: e1e0219c-f879-479f-8427-888ed2a6e9c2id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 616ad9e9b45a66f127a55ef87dd6c6b9c0b470c8
workflow-type: tm+mt
source-wordcount: 3024
ht-degree: 0%

---

# [!DNL Commerce Storefront Catalog Service]发行说明

以下发行说明涵盖最新的Commerce目录服务更新，包括：

- **[店面目录服务版本](#storefront-catalog-service)**

  - 增强了目录服务API架构以改进数据检索
  - 目录服务API和底层基础架构的安全性、性能和可靠性改进。

  有关这些API的更多信息，请参阅Commerce开发人员文档中的[Storefront Services架构](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/)。

- **[目录服务中继包版本](#catalog-service-metapackage)**

  - 更新了依赖关系，以提高性能、稳定性和与其他Adobe Commerce组件的兼容性。

- **[目录服务安装程序版本](#catalog-service-installer)**

  - 更新了依赖关系，以维护目录服务与Commerce栈栈之间的兼容性。

>[!NOTE]
>
>如果您的Commerce项目使用Adobe Commerce Optimizer将目录数据提交到Commerce Edge Delivery服务或Headless店面，请参阅[Adobe Commerce Optimizer发行说明](../optimizer/release-notes.md)以了解最新的API更新。

更新按类型分类：

![新](../assets/new.svg)新功能
![修复](../assets/fix.svg)修复和改进
![错误](../assets/bug.svg)已知问题

支持最新版本。 旧版本的发行说明包括在内，以供参考。

## 店面目录服务

## 2026年6月

**发行日期**：2026年7月1日

![新](../assets/new.svg) **新`canEditQuantity`字段** — 已将`canEditQuantity`添加到目录服务GraphQL中的`ProductViewOptionValueProduct`。 它会公开Commerce管理员中捆绑选择的可选&#x200B;**用户定义**数量设置，以便店面使用者可以确定捆绑选择的数量是否可编辑。
<!--COMOPT-2050-->

### 2026年5月

**发行日期**： 2026年5月20日
<!-- v1.55 -->

![新](../assets/new.svg)根据[记录的限制和边界](https://experienceleague.adobe.com/en/docs/commerce/optimizer/boundaries-limits)，对Adobe Commerce和Adobe Commerce as a Cloud Service客户端的每个请求强制限制最多100个SKU。
<!--DATA-7163-->

**发行日期**： 2026年5月13日
<!--v1.54-->

![新建](../assets/new.svg) **GraphQL中的类别排序顺序** — `CategoryView` GraphQL类型现在包含职位字段，因此店面可以显示目录层次结构中商家配置的订单中的类别。
<!--DATA-7166-->

**发行日期**： 2026年5月4日
<!-- v1.53 -->

![修复](../assets/fix.svg)店面产品价格现在显示所有产品类型的正确货币代码（例如，美元）。 以前，某些产品显示`NONE`而不是预期的货币，从而导致缺少价格。 此更新确保在整个店面一致且准确地呈现价格。<!--DATA-7115-->

### 2026年4月

**发行日期**：2026年4月29日
<!--v1.52-->

![新](../assets/new.svg)已强制限制Adobe Commerce Optimizer和Adobe Commerce as a Cloud Service的每个请求最多100个SKU
根据[记录的限制和边界](https://experienceleague.adobe.com/en/docs/commerce/optimizer/boundaries-limits)的客户端。<!--DATA-7156-->

**发行日期**：2026年4月17日
<!--v1.51-->

![新](../assets/new.svg)添加了一个新的`searchCategory` GraphQL查询，该查询使客户端能够按名称搜索具有分页结果的类别。 查询接受必需的`searchTerm`（至少3个字符）以及可选的`family`、`pageSize`和`currentPage`参数。 结果包括与具有完整类别元数据的`CategoryTreeView`对象、`totalCount`和分页`pageInfo`匹配。<!--COMOPT-1819-->

此查询仅适用于使用Adobe Commerce Optimizer促销服务的客户。 请参阅[searchCategory](https://developer.adobe.com/commerce/services/reference/graphql/)。

### 2026年3月

**发行日期**：2026年3月24日
<!--v1.49-->

![新](../assets/new.svg)添加了对计算并返回动态捆绑包价格范围的支持。
<!--DATA-7115-->

### 2025年12月

**发行日期**：2025年12月11日
<!-- v1.46 -->

![修复](../assets/fix.svg)系统级和基础架构改进以提高性能和稳定性。
<!--DATA-6852, DATA-6864-->

### 2025年11

**发行日期**： 2025年11月17日
<!-- v1.45 -->

![新](../assets/new.svg) **按名称筛选属性**- `productSearch` GraphQL查询现在支持使用`names`字段筛选产品属性。<!--DATA-6831--> 通过此过滤器，您可以：

- 通过仅请求特定属性减小响应有效负载大小
- 与现有`roles`筛选器结合，按可见性角色和属性名称缩小
- 示例：

  **仅按属性名称筛选**

  ```graphql
  query {
    products(skus: ["SKU-001"]) {
      attributes(names: ["color", "size", "material"]) {
        name
        label
        value
      }
    }
  }
  ```

  **按角色和名称筛选：**

  ```graphql
  query {
    products(skus: ["SKU-001"]) {
      attributes(roles: ["visible in PDP"], names: ["eco_collection", "new"]) {
        name
        label
        value
        roles
      }
    }
  }
  ```

>[!NOTE]
>
>要在不进行筛选的情况下检索所有属性，请省略`names`参数或提供空数组。

**发行日期**：2025年11月6日
<!-- v1.44 -->

![修复](../assets/fix.svg)系统级和基础架构改进以提高性能和稳定性。<!--DATA-6852, DATA-6864-->

![修复](../assets/fix.svg)当父产品无定价时，现在可以查询分组产品；子产品返回其自己的可见性角色。<!--DATA-6779-->

![修复](../assets/fix.svg)系统级和基础架构改进以提高性能和稳定性。<!--DATA-6721, DATA-6864-->

### 2025年9月

**发行日期**：2025年9月8日
<!-- v1.42 -->

![新](../assets/new.svg) **已添加层定价支持**&#x200B;以查询卷定价：<!--DATA-6643-->

要检索层定价，请执行以下操作：

1. 将`products`查询用于所需的SKU
2. 对于&#x200B;**SimpleProductView**，访问`price.tiers`
3. 对于&#x200B;**ComplexProductView**，访问`priceRange.minimum.tiers`和`priceRange.maximum.tiers`
4. 每个层包含折扣的`tier`价格和`quantity`条件
5. 使用`gte` （大于或等于）和`lt` （小于）定义数量阈值

**示例：**

```graphql
query {
  products(skus: ["SKU-001"]) {
    ... on SimpleProductView {
      price {
        regular { amount { value currency } }
        tiers {
          tier { amount { value currency } }
          quantity {
            ... on ProductViewTierRangeCondition { gte lt }
          }
        }
      }
    }
  }
}
```

![修复](../assets/fix.svg) **按最低最终价格筛选的层价格** <!--DATA-6643-->

API现在仅返回折扣价格低于产品最低最终价格&#x200B;**的层。**&#x200B;由于店面将适用最低最终价格，因此省略了较高层级。

适用于：

- **简单产品**： `price.tiers`仅包含具有`tier.amount.value` &lt; `price.final.amount.value` （最小最终值）的层。
- **复杂产品**： `priceRange.minimum.tiers`和`priceRange.maximum.tiers`在生成价格范围时使用相同的规则。

**发行日期**：2025年9月2日
<!-- v1.41 -->

![修复](../assets/fix.svg) **改进了对缺少价格信息的错误处理** — 当尚未收到价格数据时，API将返回价格字段的`null`而不是引发错误，从而允许客户端正常处理缺少的数据。<!--DATA-6612-->

![修复](../assets/fix.svg)系统级和基础架构改进以增强性能和稳定性。<!--DATA-6671-->

### 2025年7月

**发行日期**：2025年7月30日
<!-- v1.40 -->

![修复](../assets/fix.svg)系统级和基础架构改进以增强安全性、性能和稳定性。<!--DATA-6619-->

**发行日期**： 2025年7月24日
<!-- v1.39 -->

![新](../assets/new.svg) **按单位ID检索推荐单位** — 新GraphQL终结点`recommendationsByUnitIds`按单位的唯一ID检索推荐单位，以实现更灵活、更有针对性的访问。

- `unitIds`是必需的（要获取的recId列表）。
- 上下文参数(`currentSku`、`cartSkus`、`userViewHistory`、`userPurchaseHistory`、`category`)的行为与现有推荐查询中的行为相同。

- **示例**

  ```graphql
  query {
    recommendationsByUnitIds(
      unitIds: ["11ee89d1-bfae-4582-a921-2ced44ff6bf7"]
      currentSku: "24-MB01"
      cartSkus: ["24-MB01"]
    ) {
      totalResults
      results {
        unitId
        unitName
        totalProducts
        productsView {
          sku
        }
        pageType
        typeId
        storefrontLabel
        displayOrder
      }
    }
  }
  ```

![修复](../assets/fix.svg)系统级和基础架构改进以增强安全性、性能和稳定性。<!--DATA-6316-->

**发行日期**： 2025年7月15日
<!-- v1.38 -->

![新](../assets/new.svg) **礼品卡产品类型** — 目录店面服务现在支持将产品属性作为JSON对象或数组，从而灵活管理复杂类型，如礼品卡。<!--DATA-6573-->

+++先前版本

### 2025年6月

**发行日期**： 2025年6月20日
<!-- v1.37 -->

![新](../assets/new.svg) **分层价格手册配置** — 父 — 子价格手册的准确价格范围。 计算会遵循层次结构和继承的规则；在链接多个价格手册时可减少定价错误。 仅限Adobe Commerce Optimizer。 查看[价格手册](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/pricebooks)。

![新](../assets/new.svg) **不区分大小写的键** — 查询中的键查找现在不区分大小写，减少了键大小写错误。<!--DATA-6494, DCAT-2495-->

**发行日期**： 2025年6月20日
<!-- v1.36 -->

![新建](../assets/new.svg) **目录店面的公共IO事件** — 添加了用于实时集成和可观察性（CSS和EDS）的公共IO事件。<!--DATA-6329-->

![新](../assets/new.svg) **服务器端渲染(SSR)** — 体系结构改进，支持SSR以获得更大的目录性能、SEO和UX。<!--DATA-6278, DATA-6280-->

![新](../assets/new.svg) **基础架构和安全性** — 事件服务的新AWS角色、ServiceNow集成和CI/CD管道。

![新](../assets/new.svg) **事件格式和可观察性** — 简化了负载、增强了监控、改进了变量事件数据。<!--DATA-6332, DATA-6402, -->

![修复](../assets/fix.svg)系统级和基础架构改进以增强安全性、性能和稳定性。<!--DATA-6404, DATA-6410, -->

**发行日期**： 2025年6月13日
<!-- v1.35 -->

![新建](../assets/new.svg) **检索未缓存数据** — 启用`Magento-Is-Preview`标头以将未缓存数据从目录终结点传递到Search Service。<!--DATA-6345-->

![新](../assets/new.svg) **多选产品选项**-GraphQL API现在公开产品选项是否允许多选（例如，捆绑“选择多个项目”）。<!--DATA-6487-->

![新](../assets/new.svg)已更新数据摄取的价格验证以支持无价格的产品。<!--DATA-6098-->

![修复](../assets/fix.svg)改进了Adobe Commerce Optimizer中简单捆绑定价的错误处理。<!--DATA-6541-->

![修复](../assets/fix.svg)系统级和基础架构改进以增强安全性、性能和稳定性。<!--DATA-6273, DATA-6485, -->

### 2025年4月

**发行日期**：2025年4月8日
<!-- v1.34 -->

![修复](../assets/fix.svg)系统级和基础架构改进以增强安全性、性能和稳定性。<!--DATA-5732-->

<!-- v1.33 -->
![Fix](../assets/fix.svg)基础架构现在支持非常大的目录（最多约4.4亿SKU），而不影响现有工作负载。

### 2025年3月

**发行日期**： 2025年3月28日
<!-- v1.32 -->

![修复](../assets/fix.svg)对于可组合目录，没有角色的属性在默认情况下不再编制索引，从而缩短索引时间并减小存储空间。 可以通过功能标记重新启用旧版行为。

![修复](../assets/fix.svg)系统级和基础架构改进以增强安全性、性能和稳定性。
<!--DATA-6348, DATA-6440, DATA-6446, DATA-6641-->

### 2025年2月

**发行日期**： 2025年2月18日
<!-- v1.31 -->

![修复](../assets/fix.svg)系统级和基础架构改进以增强安全性、性能和稳定性。<!--DATA-6389, DATA-6367, DATA-6373-->

### 2024年12月

**发行日期**： 2024年12月9日
<!-- v1.30 -->

主要版本：用于Headless店面、标题管理和产品数据处理的[可组合目录数据模型](https://developer.adobe.com/commerce/services/optimizer/)。

![新](../assets/new.svg) **可组合目录数据模型(CCDM)** — 支持客户将可组合目录用于Headless店面。 新端点接受目录视图和策略ID（向后兼容）。 具有内置分页的可配置产品详细信息和价格。<!--DATA-6018, DATA-6288-->

对于可组合目录API操作，![新建](../assets/new.svg) **标头管理**-`AC-Locale`已重命名为`AC-Scope-Locale`；指定了标头映射和默认值。<!--DATA-6303, DATA-6078-->

![新](../assets/new.svg) **产品数据和定价** — 支持可组合目录数据模型和改进可配置产品的价格处理。<!--DATA-6279-->

`CurrencyEnum`已更新，以支持`NONE`的产品搜索查询，并与联合逻辑保持一致。<!--DATA-6285-->

![修复](../assets/fix.svg) **基础架构和升级** — 安全性、性能和稳定性的系统级改进。

![修复](../assets/fix.svg)捆绑包产品选项现在仅显示启用的产品。<!--DATA-6347-->

**发行日期**： 2024年12月9日
<!-- v1.29 -->

![新](../assets/new.svg) **产品查询中的图像排序**—GraphQL `images`字段中的产品图像现在遵循目录导出`sortOrder`，以便店面和API行为一致。<!--DATA-6258-->

![修复](../assets/fix.svg)系统级和基础架构改进以增强安全性、性能和稳定性。<!--DATA-6619-->

**发行日期**：2024年12月
<!-- v1.28 -->

![修复](../assets/fix.svg)系统级和基础架构改进以增强安全性、性能和稳定性。
<!--DATA-6180, DATA-6230, DATA-6254, DATA-6257-->

### 2024年10

**发行日期**：2024年10月22日
<!-- v1.26 -->

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg) GraphQL架构现在在产品信息中包含`lastModifiedAt`，以便获得准确的站点地图和搜索引擎重新索引（例如，Google）。
<!--DATA-6209-->

### 2024年9月

**发行日期**： 2024年9月26日
<!-- v1.27 -->

![修复](../assets/fix.svg)系统级和基础架构改进以增强安全性、性能和稳定性。
<!--DATA-6243-->

### 2024年8月

**发行日期**： 2024年8月22日
<!-- v1.23 -->

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![修复](../assets/fix.svg)现在无需产品覆盖（价格）数据即可检索产品信息。 以前，这些查询返回： `The following sku does not have product override data in the DB: <SKU value>. Make sure data is synced.`
<!--DATA-6121-->

**发行日期**： 2024年8月13日
<!-- v1.22 -->

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)添加了对按产品SKU检索所有变体的支持。 请参阅[目录服务API引用](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)。
<!--DATA-6067-->

### 2024年5月

**发行日期**： 2024年5月23日
<!-- v1.19 -->

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本


![修复](../assets/fix.svg)选项值的`InStock`标记现在遵循产品变体的作用域`enabled`状态。

<!--DATA-5033-->

![Fix](../assets/fix.svg)添加了对产品价格的支持，最高可支持16位和4位小数。 从[数据管理仪表板](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)或[CLI](../data-export/data-export-cli-commands.md)重新同步以应用更新。
<!--DATA-5033-->

#### 已知限制

尚不支持以下功能：

- 动态属性有效负载的最大大小为9 MB。
- 本集团产品价格可按简单产品价格计算。
- 在图像数组中，只有第一个图像包含角色。

将API Mesh和核心GraphQL API用于：

- 最低广告价格
- 分层定价
- 捆绑固定价格的产品

有关详细信息和示例，请参阅[目录服务和API网格](mesh.md)。

### 2024年4月

**发行日期**： 2024年4月11日
<!-- v1.18 -->

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)添加了对PHP 8.3的支持。

![新](../assets/new.svg) [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/)和[`refineProduct`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/)查询现在返回简单和复杂产品的可自定义选项数据。<!--DATA-5538-->

### 2024年2月

**发行日期**： 2024年2月22日
<!-- v1.17 -->

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg) [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html)现在可用于数据流（产品推荐、实时搜索、目录服务）。 需要`catalog-service`个中继包v3.1.0+。

**发行日期**： 2024年2月13日
<!-- v1.16 -->

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

目录服务API现在支持![新](../assets/new.svg)产品视频。
![修复](../assets/fix.svg)缺货的期权现在显示在PDP小部件中。

#### 已知限制

尚不支持以下功能：

- 动态属性有效负载的最大大小为9 MB。
- 组产品价格。 此值可使用简单的产品价格计算。
- 在图像数组中，只有第一个图像包含角色。

将API Mesh和核心GraphQL API用于：

- 最低广告价格
- [分层定价](mesh.md)

### 2023年10

**发行日期**：2023年10月12日
<!-- v1.13 -->

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)目录服务支持产品变体的`inStock`标志。
![新](../assets/new.svg) `urlKey`和`externalId`字段已添加到GraphQL架构中。
现在支持![新](../assets/new.svg)可下载的产品和礼品卡。

### 2023年9月

**发行日期**： 2023年9月19日
<!-- v1.12 -->

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)目录服务现在使用[SaaS价格索引](../price-index/price-indexing.md)。
![修复](../assets/fix.svg)此版本包含服务端的错误修复和改进。

### 2023年7月

**发行日期**： 2023年7月18日
<!-- v1.11 -->

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)目录服务现在支持产品推荐的[`recommendations`](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/) GraphQL查询。

### 2023年6月

**发行日期**： 2023年6月27日
<!-- v1.10 -->

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)目录服务API现在支持`related products`。

### 2023年4月

**发行日期**： 2023年4月12日
<!-- v1.7 -->

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)目录服务现在正在清理已删除的产品变体。
![修复](../assets/fix.svg)基础架构可扩展性和性能改进。

### 2023年3月

**发行日期**： 2023年3月28日
<!-- v1.6 -->

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)已将样本添加到[`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/)查询。
![新](../assets/new.svg)已添加使用[API Mesh](mesh.md)获取`entityId`的功能。

**发行日期**： 2023年3月6日
<!-- v1.5 -->

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)添加了[`categories`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/)个GraphQL功能。
![修复](../assets/fix.svg)改进了性能和API可扩展性。

### 2023年2月

**发行日期**： 2023年2月7日
<!-- v1.4 -->

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![新建](../assets/new.svg)已发布的目录服务中继包以简化安装步骤。
![修复](../assets/fix.svg) API可扩展性和性能改进。

### 2023年1月

**发行日期**： 2023年1月17日
<!-- v1.3 -->

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![新](../assets/new.svg)简化并改进了入门体验。
![新](../assets/new.svg)新客户沙盒端点可用于预生产测试。
已为虚拟产品添加![新](../assets/new.svg)支持。
![修复](../assets/fix.svg) API可扩展性和性能改进。

### 2022年11

**发行日期**： 2022年11月18日
<!-- v1.1 -->

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![新](../assets/new.svg)目录服务现在支持Adobe的[API网格](https://developer.adobe.com/graphql-mesh-gateway/)。
![修复](../assets/fix.svg)改进了API可扩展性和整体性能。

### 2022年10

**发行日期**： 2022年10月4日
<!-- v1.0 -->

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

对捆绑产品和分组产品的![新](../assets/new.svg)支持。
![新](../assets/new.svg)添加了B2B可见性覆盖。 产品现在可供搜索，并可添加到特定客户组的购物车中。
![Fix](../assets/fix.svg)服务现在更稳定，性能也有所提高。

### 2022年9月

**发行日期**： 2022年9月12日
<!-- v0.3 -->

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![新](../assets/new.svg)变体图像：根据所选选项返回的产品图像。
![新](../assets/new.svg)价格角色：只有特定客户组的成员才能看到产品价格。
![修复](../assets/fix.svg)提高了服务的稳定性和性能。
从目录中删除产品时收到![个新](../assets/new.svg)更新。

### 2022年8月

**发行日期**： 2022年8月9日
<!-- Beta -->

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![新](../assets/new.svg) `products`和`refineProduct`查询返回以下数据：

- 预定义的（系统）产品属性。
- 动态产品属性，并按角色（产品显示页面/产品列表页面）筛选这些属性。
- 产品选项。
- 产品图像并按角色(PDP/PLP)过滤它们。
- 简单产品的具体价格以及可配置产品的价格范围。
- 客户组价格及价格范围。 它们向没有客户群组的购物者返还后备默认价格。
- 使用B2B客户特定定价的产品类型。

+++

## 目录服务中继

目录服务PHP中继(`magento/catalog-service`)的更新。

- 对于Adobe Commerce as a Cloud Service客户，您的环境中安装了最新版本。

- 对于云上或内部部署的Adobe Commerce，Adobe建议使用编辑器升级云环境中的目录服务中继（最新版本）。

### v3.5.0发布

**发行日期**：2026年7月10日

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新建](../assets/new.svg) **暂存类别URL密钥同步** — 已更新目录服务中继包依赖关系，以包括目录暂存数据导出器模块(`magento/module-catalog-staging-data-exporter`)。 当应用暂存类别`url_key`更改时，此模块会重新导出产品馈送，因此暂存目录更改会正确传播到SaaS目录（目录服务、实时搜索和产品推荐）。

![新](../assets/new.svg)更新了依赖关系，以保持目录服务与Commerce栈栈之间的兼容性。

### v3.4.0发布

**发行日期**： 2026年6月8日

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg) **支持数据馈送同步状态监视** — 已更新目录服务中继包依赖项以包括数据导出器状态扩展(`magento/module-data-exporter-status`)。 这将启用Commerce Admin中的[数据馈送同步状态监视](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status)，而无需执行任何其他安装或配置步骤

![新](../assets/new.svg)更新了依赖关系，以保持目录服务与Commerce栈栈之间的兼容性。

### v3.3.0发布

**发行日期**：2025年10月14日

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg) **数据服务升级**—`magento/data-services`依赖关系已更新为^8.0.0。 在升级之前，验证环境和自定义数据服务API的使用情况以实现8.x兼容性。

![新](../assets/new.svg)更新了3.3.0版本的版本和元数据。

### v3.2.0发布

**发行日期**： 2024年4月12日

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

已为3.2.0更新![新](../assets/new.svg)版本和元数据。 没有其他依赖关系更改。

### v3.1.0发布

**发行日期**： 2024年1月26日

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)已添加新的包依赖项：

- **类别权限数据导出器** (`magento/module-category-permission-data-exporter`)，用于导出目录服务使用的类别权限数据。
- **目录同步管理员** `magento/module-catalog-sync-admin`，用于与目录同步相关的管理员UI和配置。

![新](../assets/new.svg)更新了3.1.0版本的版本和元数据。

## 目录服务安装程序

安装程序随目录服务扩展一起提供，并处理安装和环境检查，以使目录服务与您的Commerce栈栈匹配。

- 对于&#x200B;**Adobe Commerce as a Cloud Service**&#x200B;客户，您的环境中安装了最新安装程序版本。

- 对于云基础架构上的&#x200B;**Adobe Commerce**&#x200B;或&#x200B;**内部部署**，使安装程序与[目录服务中间包](#catalog-service-metapackage)保持一致。

无论何时使用编辑器升级`magento/catalog-service`，安装程序包都会自动更新为最新版本。 当这些发行说明描述所需的更改（例如，支持新的PHP版本）时，您也可以使用Composer单独升级`magento/catalog-service-installer`。 这样，您的安装工具就会与您运行的目录服务版本保持兼容。

### v1.0.6发布

**发行日期**：2026年3月25日

![New](../assets/new.svg) **PHP 8.5** — 确保目录服务在PHP 8.5上运行时兼容。

## 相关文档

- 对于在**Adobe Commerce on cloud、内部部署或Adobe Commerce as a Cloud Service上部署的项目，请参阅以下文档：

  - [目录服务指南](overview.md)
  - [目录服务GraphQL API参考](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)
  - [Adobe Commerce管理指南](https://experienceleague.adobe.com/en/docs/commerce-admin/)
  - [Adobe Commerce as a Cloud Service指南](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/)
  - [Adobe Commerce on Cloud指南](https://experienceleague.adobe.com/en/docs/commerce-cloud/)

- 对于使用&#x200B;**Adobe Commerce Optimizer**&#x200B;或&#x200B;**Adobe Commerce Optimizer Connector**&#x200B;的项目，请参阅以下文档：

  - [Merchandising Services开发人员指南](https://developer.adobe.com/commerce/services/optimizer/)
  - [促销GraphQL API参考](https://developer.adobe.com/commerce/services/reference/graphql/)
  - [Adobe Commerce Optimizer指南](../optimizer/overview.md)
