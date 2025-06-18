---
title: '[!DNL Catalog Service]发行说明'
description: Adobe Commerce的 [!DNL Catalog Service] 的最新发行信息。
feature: Services, Catalog Service, Release Notes
exl-id: 74f2e46a-5592-4857-a6d7-b95b85d8b4cc
source-git-commit: fe5f864262478d1f9e205f2cd275452594cf4675
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 0%

---

# [!DNL Catalog Service]发行说明

以下发行说明介绍了[!DNL Catalog Service]的最新版本。
为当前的主要发行版本提供支持。 提供了旧版本的发行说明以供参考。
更新包括：

![新](../assets/new.svg)新功能
![修复](../assets/fix.svg)修复和改进
![错误](../assets/bug.svg)已知问题

## 当前主要版本

### V1.26发布

_2024年10月22日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg) GraphQL架构现在在产品信息中包含`lastModifiedAt`属性。 此准确的时间戳可帮助客户确保站点地图准确反映其产品的最新更新。 此外，它还有助于诸如Google之类的搜索引擎确定何时需要重新索引，优化搜索过程并防止在无法获取准确信息时使用积极的上次修改日期时出现问题。<!--DATA-6209-->

## 先前版本

+++ 先前版本

### V1.23发布

_2024年8月22日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![修复](../assets/fix.svg)您现在可以检索产品信息，而无需产品覆盖（价格）数据。 在以前的版本中，这些查询返回以下错误：
`The following sku does not have product override data in the DB: <SKU value>. Make sure data is synced.` <!--DATA-6121-->

### V1.22发布

_2024年8月13日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)添加了对按产品SKU检索所有变体的支持。 查看[目录服务API引用](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)。<!--DATA-6067-->

### V1.22发布

_2024年8月13日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)添加了对按产品SKU检索所有变体的支持。 查看[目录服务API引用](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)。<!--DATA-6067-->

### V1.19发布

_2024年5月23日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本


![修复](../assets/fix.svg) <!--DATA-5033-->选项值的`InStock`标志现在会考虑产品变体的作用域`enabled`状态。

![修复](../assets/fix.svg) <!--DATA-5888-->添加对需要大数字（最多16位）和高小数精度（最多4位小数）的产品价格的支持。 要将价格配置更新应用到现有目录，请从[数据管理仪表板](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/systems/data-transfer/data-dashboard)重新同步目录数据，或使用[Adobe Commerce命令行界面](../landing/catalog-sync.md#command-line-interface)重新同步目录数据。

#### 已知限制

尚不支持以下功能：

* 动态属性有效负载的最大大小为9 MB。
* 本集团产品价格可按简单产品价格计算。
* 在图像数组中，只有第一个图像包含角色。

通过使用API Mesh和核心GraphQL API解决以下限制：

* 最低广告价格
* 分层定价
* 捆绑固定价格的产品

有关详细信息和示例，请参阅[目录服务和API网格](mesh.md)

### V1.18发布

_2024年4月11日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)添加了对PHP 8.3的支持。

![新](../assets/new.svg) [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/)和[`refineProduct`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/)查询现在返回简单和复杂产品的可自定义选项数据。<!--DATA-5538-->

### V1.17发布

_2024年2月22日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg) [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-dashboard.html?lang=zh-Hans)现已可用。 此改版后的仪表板提供[!DNL Product Recommendations]、[!DNL Live Search]和[!DNL Catalog Service]的数据流分析。 `catalog-service`中继v3.1.0中引入了对此功能的支持。

### V1.16发布

_2024年2月13日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

目录服务API现在支持![新](../assets/new.svg)产品视频。
![修复](../assets/fix.svg)缺货的期权现在显示在PDP小部件中。

#### 已知限制

尚不支持以下功能：

* 动态属性有效负载的最大大小为9 MB。
* 组产品价格。 此值可使用简单的产品价格计算。
* 在图像数组中，只有第一个图像包含角色。

使用API Mesh和核心GraphQL API可以解决以下限制：

* 最低广告价格
* [分层定价](mesh.md)

### V1.13发布

_2023年10月12日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)目录服务支持产品变体的`inStock`标志。
![新](../assets/new.svg) `urlKey`和`externalId`字段已添加到GraphQL架构中。
现在支持![新](../assets/new.svg)可下载的产品和礼品卡。

### V1.12发布

_2023年9月19日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)目录服务现在使用[SaaS价格索引](../price-index/price-indexing.md)。
![修复](../assets/fix.svg)此版本包含服务端的错误修复和改进。

### V1.11发布

_2023年7月18日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)目录服务现在支持产品推荐的[`recommendations`](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/recommendations/) GraphQL查询。

### V1.10发布

_2023年6月27日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)目录服务API现在支持`related products`。

### V1.7发布

_2023年4月12日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)目录服务现在正在清理已删除的产品变体。
![修复](../assets/fix.svg)基础架构可扩展性和性能改进。

### V1.6发布

_2023年3月28日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)已将样本添加到[`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/)查询。
![新](../assets/new.svg)已添加使用[API Mesh](mesh.md)获取`entityId`的功能。

### V1.5发布

_2023年3月6日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)添加了[`categories`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/)个GraphQL功能。
![修复](../assets/fix.svg)改进了性能和API可扩展性。

### V1.4发布

_2023年2月7日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![新建](../assets/new.svg)已发布的目录服务中继包以简化安装步骤。
![修复](../assets/fix.svg) API可扩展性和性能改进。

### V1.3发布

_2023年1月17日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![新](../assets/new.svg)简化并改进了入门体验。
![新](../assets/new.svg)新客户沙盒端点可用于预生产测试。
已为虚拟产品添加![新](../assets/new.svg)支持。
![修复](../assets/fix.svg) API可扩展性和性能改进。

### V1.1发布

_2022年11月18日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![新](../assets/new.svg)目录服务现在支持Adobe的[API网格](https://developer.adobe.com/graphql-mesh-gateway/)。
![修复](../assets/fix.svg)改进了API可扩展性和整体性能。

### V1.0发布

_2022年10月4日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![新](../assets/new.svg)现在支持捆绑和分组的产品。
![新](../assets/new.svg)添加了B2B可见性覆盖。 产品现在可供搜索，并可添加到特定客户组的购物车中。
![Fix](../assets/fix.svg)服务现在更稳定，性能也有所提高。

### 0.3版本 — Beta+

_2022年9月12日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![新](../assets/new.svg)支持变体的图像：根据所选选项返回产品图像
![新](../assets/new.svg)价格角色支持：仅允许特定客户组的成员查看产品价格
![修复](../assets/fix.svg)提高了服务的稳定性和性能
从目录中删除产品时收到![个新](../assets/new.svg)更新

### Beta版本

_2022年8月9日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![新](../assets/new.svg) `products`和`refineProduct`查询返回以下数据：

* 预定义的（系统）产品属性。
* 动态产品属性，并按角色（产品显示页面/产品列表页面）筛选这些属性。
* 产品选项。
* 产品图像并按角色(PDP/PLP)过滤它们。
* 简单产品的具体价格以及可配置产品的价格范围。
* 客户组价格及价格范围。 它们向没有客户群组的购物者返还后备默认价格。
* 使用B2B客户特定定价的产品类型。
