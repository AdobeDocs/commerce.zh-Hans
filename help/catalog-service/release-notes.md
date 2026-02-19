---
title: '[!DNL Commerce Storefront Catalog Service Release Notes]'
description: Adobe Commerce的 [!DNL Catalog Service] 的最新发行信息。
feature: Services, Catalog Service, Release Notes
exl-id: 74f2e46a-5592-4857-a6d7-b95b85d8b4cc
source-git-commit: 9ba7a964243c616cc7e40fb180a855b839cd4597
workflow-type: tm+mt
source-wordcount: '2252'
ht-degree: 0%

---

# [!DNL Commerce Storefront Catalog Service]发行说明

以下发行说明涵盖最新的Commerce目录服务更新，包括：

- **店面目录服务版本**

   - 目录服务API架构增强，改进了数据检索。
   - 目录服务API和底层基础架构的安全性、性能和可靠性改进。

- **目录服务中继包版本**

   - 更新了依赖关系，以提高性能、稳定性和与其他Adobe Commerce组件的兼容性。

更新按类型分类：

![新](../assets/new.svg)新功能
![修复](../assets/fix.svg)修复和改进
![错误](../assets/bug.svg)已知问题

支持最新版本。 旧版本的发行说明包括在内，以供参考。

## 店面目录服务

### v1.48发布

_2025年2月19日_

![新建](../assets/new.svg) GraphQL API中的`categoryTree`查询现在返回类别描述、图像和SEO元标记。 此更新提供了店面开发人员显示类别图像所需的数据，并通过适当的元标题、描述和关键词改进了搜索引擎优化。 仅在Commerce实施上受支持，使用用于Headless店面&lt;[的](https://developer.adobe.com/commerce/services/optimizer/)可组合目录数据模型<!--DATA-6933-->

### v1.47发布

_2025年2月12日_

![新](../assets/new.svg) API服务现在支持`CategoryProductView`类型，支持按类别对产品进行增强的视图和查询。 此更新使开发人员能够根据类别高效地检索和筛选产品数据，从而提高类别驱动用例的灵活性和性能。 有关详细信息，请参阅[在店面上实施类别](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/categories-storefront-implementation/)。 仅在Commerce实施上支持使用[针对Headless店面](https://developer.adobe.com/commerce/services/optimizer/)的可组合目录数据模型<!--DATA-6949-->

### v1.46发布

_2025年12月11日_

![修复](../assets/fix.svg)系统级和基础架构改进以提高性能和稳定性。<!--DATA-6852, DATA-6864-->

### v1.45发布

_2025年11月17日_

![新](../assets/new.svg) **按名称筛选属性**- `productSearch` GraphQL查询现在支持使用`names`字段筛选产品属性。 <!--DATA-6831-->使用此筛选器，您可以：

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

### v1.44发布

_2025年11月6日_

![修复](../assets/fix.svg)系统级和基础架构改进以提高性能和稳定性。<!--DATA-6852, DATA-6864-->

### v1.43发布

_2025年11月3日_

![新](../assets/new.svg) **多维产品自定义的产品层** — 为Adobe Commerce Optimizer实施添加了对特定于渠道的区域设置感知内容交付的支持。<!--DATA-6632-->

- 为不同的客户群提供不同的产品内容
- 应用特定于区域设置的自定义项而不复制基础数据
- 使用图层蒙版控制字段级覆盖
- 支持针对高级、季节和移动设备优化的内容层

  使用现有`products`查询检索图层，从请求标头在服务器端应用，无需更改架构。 请参阅[Adobe Commerce Optimizer指南](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/catalog-layer)中的&#x200B;_目录层_。

![修复](../assets/fix.svg)当父产品无定价时，现在可以查询分组产品；子产品返回其自己的可见性角色。<!--DATA-6779-->

![修复](../assets/fix.svg)系统级和基础架构改进以提高性能和稳定性。<!--DATA-6721, DATA-6864-->

### v1.42发布

_2025年9月8日_

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

### v1.41发布

_2025年9月2日_

![修复](../assets/fix.svg) **改进了对缺少价格信息的错误处理** — 当尚未收到价格数据时，API将返回价格字段的`null`而不是引发错误，从而允许客户端正常处理缺少的数据。<!--DATA-6612-->

![修复](../assets/fix.svg)系统级和基础架构改进以增强性能和稳定性。<!--DATA-6671-->

### v1.40发布

_2025年7月30日_

![修复](../assets/fix.svg)系统级和基础架构改进以增强安全性、性能和稳定性。<!--DATA-6619-->

### v1.39发布

_2025年7月24日_

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

### v1.38发布

_2025年7月15日_

![新](../assets/new.svg) **礼品卡产品类型** — 目录店面服务现在支持将产品属性作为JSON对象或数组，从而灵活管理复杂类型，如礼品卡。<!--DATA-6573-->


### v1.37发布

_2025年6月20日_

![新](../assets/new.svg) **分层价格手册配置** — 父 — 子价格手册的准确价格范围。 计算会遵循层次结构和继承的规则；在链接多个价格手册时可减少定价错误。 仅限Adobe Commerce Optimizer。 查看[价格手册](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/pricebooks)。

![新](../assets/new.svg) **不区分大小写的键** — 查询中的键查找现在不区分大小写，减少了键大小写错误。<!--DATA-6494, DCAT-2495-->

### v1.36发布

_2025年6月20日_

![新建](../assets/new.svg) **目录店面的公共IO事件** — 添加了用于实时集成和可观察性（CSS和EDS）的公共IO事件。<!--DATA-6329-->

![新](../assets/new.svg) **服务器端渲染(SSR)** — 体系结构改进，支持SSR以获得更大的目录性能、SEO和UX。<!--DATA-6278, DATA-6280-->

![新](../assets/new.svg) **基础架构和安全性** — 事件服务的新AWS角色、ServiceNow集成和CI/CD管道。

![新](../assets/new.svg) **事件格式和可观察性** — 简化了负载、增强了监控、改进了变量事件数据。<!--DATA-6332, DATA-6402, -->

![修复](../assets/fix.svg)系统级和基础架构改进以增强安全性、性能和稳定性。<!--DATA-6404, DATA-6410, -->

+++ 先前版本

## v1.35发布

_2025年6月13日_

![新建](../assets/new.svg) **检索未缓存数据** — 启用`Magento-Is-Preview`标头以将未缓存数据从目录终结点传递到Search Service。<!--DATA-6345-->

![新](../assets/new.svg) **多选产品选项**-GraphQL API现在公开产品选项是否允许多选（例如，捆绑“选择多个项目”）。<!--DATA-6487-->

![新](../assets/new.svg)已更新数据摄取的价格验证以支持无价格的产品。<!--DATA-6098-->

![修复](../assets/fix.svg)改进了Adobe Commerce Optimizer中简单捆绑定价的错误处理。<!--DATA-6541-->

![修复](../assets/fix.svg)系统级和基础架构改进以增强安全性、性能和稳定性。<!--DATA-6273, DATA-6485, -->

## v1.34发布

_2025年3月23日_

![修复](../assets/fix.svg)系统级和基础架构改进以增强安全性、性能和稳定性。<!--DATA-5732-->

## v1.33发布

_2025年4月29日_

![修复](../assets/fix.svg)系统级和基础架构改进。 基础架构现在支持非常大的目录（最多达4.4亿SKU），而不影响现有工作负载。

### v1.32发布

_2025年3月28日_

![修复](../assets/fix.svg)对于可组合目录，没有角色的属性在默认情况下不再编制索引，从而缩短索引时间并减小存储空间。 可以通过功能标记重新启用旧版行为。

![修复](../assets/fix.svg)系统级和基础架构改进以增强安全性、性能和稳定性。<!--DATA-6348, DATA-6440, DATA-6446, DATA-6641-->

### v1.31发布

_2025年2月18日_

![修复](../assets/fix.svg)系统级和基础架构改进以增强安全性、性能和稳定性。<!--DATA-6389, DATA-6367, DATA-6373-->

### v1.30发布

_2024年12月9日_

主要版本：用于Headless店面、标题管理和产品数据处理的[可组合目录数据模型](https://developer.adobe.com/commerce/services/optimizer/)。

![新](../assets/new.svg) **可组合目录数据模型(CCDM)** — 支持客户将可组合目录用于Headless店面。 新端点接受目录视图和策略ID（向后兼容）。 具有内置分页的可配置产品详细信息和价格。<!--DATA-6018, DATA-6288-->

对于可组合目录API操作，![新建](../assets/new.svg) **标头管理**-`AC-Locale`已重命名为`AC-Scope-Locale`；指定了标头映射和默认值。<!--DATA-6303, DATA-6078-->

![新](../assets/new.svg) **产品数据和定价** — 支持可组合目录数据模型和改进可配置产品的价格处理。<!--DATA-6279-->

`CurrencyEnum`已更新，以支持`NONE`的产品搜索查询，并与联合逻辑保持一致。<!--DATA-6285-->

![修复](../assets/fix.svg) **基础架构和升级** — 安全性、性能和稳定性的系统级改进。

![修复](../assets/fix.svg)捆绑包产品选项现在仅显示启用的产品。<!--DATA-6347-->

### v1.29发布

_2024年12月9日_

![新](../assets/new.svg) **产品查询中的图像排序**—GraphQL `images`字段中的产品图像现在遵循目录导出`sortOrder`，以便店面和API行为一致。<!--DATA-6258-->

![修复](../assets/fix.svg)系统级和基础架构改进以增强安全性、性能和稳定性。<!--DATA-6619-->

### v1.28发布

![修复](../assets/fix.svg)系统级和基础架构改进以增强安全性、性能和稳定性。<!--DATA-6180, DATA-6230, DATA-6254, DATA-6257-->

### v1.27发布

_2024年9月26日_

![修复](../assets/fix.svg)系统级和基础架构改进以增强安全性、性能和稳定性。<!--DATA-6243-->

### v1.26发布

_2024年10月22日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg) GraphQL架构现在在产品信息中包含`lastModifiedAt`，以便获得准确的站点地图和搜索引擎重新索引(例如，Google)。<!--DATA-6209-->

### v1.23发布

_2024年8月22日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![修复](../assets/fix.svg)现在无需产品覆盖（价格）数据即可检索产品信息。 以前，这些查询返回： `The following sku does not have product override data in the DB: <SKU value>. Make sure data is synced.` <!--DATA-6121-->

### v1.22发布

_2024年8月13日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)添加了对按产品SKU检索所有变体的支持。 查看[目录服务API引用](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)。<!--DATA-6067-->

### v1.19发布

_2024年5月23日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本


![修复](../assets/fix.svg) <!--DATA-5033-->选项值的`InStock`标记现在遵循产品变体的作用域`enabled`状态。

![修复](../assets/fix.svg) <!--DATA-5888-->添加了对产品价格的支持，最高可支持16位和4位小数。 从[数据管理仪表板](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)或[CLI](../landing/catalog-sync.md#command-line-interface)重新同步以应用更新。

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

### v1.18发布

_2024年4月11日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)添加了对PHP 8.3的支持。

![新](../assets/new.svg) [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/)和[`refineProduct`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/)查询现在返回简单和复杂产品的可自定义选项数据。<!--DATA-5538-->

### v1.17发布

_2024年2月22日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg) [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html)现在可用于数据流（产品推荐、实时搜索、目录服务）。 需要`catalog-service`个中继包v3.1.0+。

### v1.16发布

_2024年2月13日_

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

### v1.13发布

_2023年10月12日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)目录服务支持产品变体的`inStock`标志。
![新](../assets/new.svg) `urlKey`和`externalId`字段已添加到GraphQL架构中。
现在支持![新](../assets/new.svg)可下载的产品和礼品卡。

### v1.12发布

_2023年9月19日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)目录服务现在使用[SaaS价格索引](../price-index/price-indexing.md)。
![修复](../assets/fix.svg)此版本包含服务端的错误修复和改进。

### v1.11发布

_2023年7月18日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)目录服务现在支持产品推荐的[`recommendations`](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/) GraphQL查询。

### v1.10发布

_2023年6月27日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)目录服务API现在支持`related products`。

### v1.7发布

_2023年4月12日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)目录服务现在正在清理已删除的产品变体。
![修复](../assets/fix.svg)基础架构可扩展性和性能改进。

### v1.6发布

_2023年3月28日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)已将样本添加到[`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/)查询。
![新](../assets/new.svg)已添加使用`entityId`API Mesh[获取](mesh.md)的功能。

### v1.5发布

_2023年3月6日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)添加了[`categories`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/)个GraphQL功能。
![修复](../assets/fix.svg)改进了性能和API可扩展性。

### v1.4发布

_2023年2月7日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![新建](../assets/new.svg)已发布的目录服务中继包以简化安装步骤。
![修复](../assets/fix.svg) API可扩展性和性能改进。

### v1.3发布

_2023年1月17日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![新](../assets/new.svg)简化并改进了入门体验。
![新](../assets/new.svg)新客户沙盒端点可用于预生产测试。
已为虚拟产品添加![新](../assets/new.svg)支持。
![修复](../assets/fix.svg) API可扩展性和性能改进。

### v1.1发布

_2022年11月18日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![新](../assets/new.svg)目录服务现在支持Adobe的[API网格](https://developer.adobe.com/graphql-mesh-gateway/)。
![修复](../assets/fix.svg)改进了API可扩展性和整体性能。

### v1.0发布

_2022年10月4日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

对捆绑产品和分组产品的![新](../assets/new.svg)支持。
![新](../assets/new.svg)添加了B2B可见性覆盖。 产品现在可供搜索，并可添加到特定客户组的购物车中。
![Fix](../assets/fix.svg)服务现在更稳定，性能也有所提高。

### 0.3版本 — Beta+

_2022年9月12日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![新](../assets/new.svg)变体图像：根据所选选项返回的产品图像。
![新](../assets/new.svg)价格角色：只有特定客户组的成员才能看到产品价格。
![修复](../assets/fix.svg)提高了服务的稳定性和性能。
从目录中删除产品时收到![个新](../assets/new.svg)更新。

### Beta版本

_2022年8月9日_

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

- 对于云内部部署的Adobe Commerce，Adobe建议使用编辑器升级云环境中的目录服务中继（最新版本）。

### v3.3.0发布

_2025年10月14日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg) **数据服务升级**—`magento/data-services`依赖关系已更新为^8.0.0。在升级之前，验证环境和自定义数据服务API的使用情况以实现8.x兼容性。
ea
![新](../assets/new.svg)更新了3.3.0版本的版本和元数据。

### v3.2.0发布

_2024年4月12日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

已为3.2.0更新![新](../assets/new.svg)版本和元数据。没有其他依赖关系更改。

### v3.1.0发布

_2024年1月26日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)已添加新的包依赖项：

- **类别权限数据导出器** (`magento/module-category-permission-data-exporter`)，用于导出目录服务使用的类别权限数据。
- **目录同步管理员** `magento/module-catalog-sync-admin`，用于与目录同步相关的管理员UI和配置。

![新](../assets/new.svg)更新了3.1.0版本的版本和元数据。

## 相关文档

- 对于在**Adobe Commerce on cloud、内部部署或Adobe Commerce as a Cloud Service上部署的项目，请参阅以下文档：

   - [目录服务指南](overview.md)
   - [目录服务GraphQL API引用](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)
   - [Adobe Commerce管理指南](https://experienceleague.adobe.com/en/docs/commerce-admin/)
   - [Adobe Commerce as a Cloud Service指南](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/)
   - 云指南上的[Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-cloud/)

- 对于使用&#x200B;**Adobe Commerce Optimizer**&#x200B;或&#x200B;**Adobe Commerce Optimizer Connector**&#x200B;的项目，请参阅以下文档：

   - [Merchandising Services开发人员指南](https://developer.adobe.com/commerce/services/optimizer/)
   - [推销GraphQL API引用](https://developer.adobe.com/commerce/services/reference/graphql/)
   - [Adobe Commerce Optimizer指南](../optimizer/overview.md)
