---
title: 边界和限制
description: 了解 [!DNL Product Recommendations] 的界限和限制，以确保它满足您的业务需求。
role: Admin, Developer
source-git-commit: 66830c9d950a27269aca1bda0dcc7d0d86f05647
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 0%

---

# 边界和限制

查看以下边界和限制以确保[!DNL Product Recommendations]满足您的业务需求。 了解这些限制有助于您规划实施、配置过滤器并避免常见问题。

## 常规

- **产品类型** — 支持的产品类型包括&#x200B;_简单_、_可配置_、_虚拟_、_可下载_&#x200B;和&#x200B;_礼品卡_。 不支持&#x200B;_捆绑包_、_分组_&#x200B;和自定义产品类型。 如果您的目录包含大量不受支持的产品类型，则[就绪性分数](create.md#readiness-indicators)可能较低。 请参阅[按产品类型筛选](filters.md#type)。
- **包含空格的SKU** — 包含空格的SKU可能会降低推荐相关性，应尽可能避免使用。
- **购物车页面** — 当您的商店配置为将产品添加到购物车后立即[显示购物车页面时，购物车页面不支持产品推荐](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/stores-sales/point-of-purchase/cart/cart-configuration)。 请参阅[创建推荐](create.md)。
- **子产品** — 可配置产品的子产品（可见性&#x200B;_不可见_）未显示在推荐单元中。 只能显示可配置（父）产品。 查看[筛选产品](filters.md#product)。
- **已禁用或不可见的产品** — 单独禁用或不可见的产品永远不会出现在推荐中，也不能在产品筛选器中选择。
- 推荐单位中不支持具有开始和结束日期的&#x200B;**特殊定价** - [特殊价格](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/catalog/products/pricing/product-price-special)。 具有特殊价格的产品可能会出现在推荐中，但单位不显示特殊价格、开始日期或结束日期。 在打开产品页面之前，购物者会看到常规价格（或您的目录/价格信息源提供的其他价格数据）。

## 推荐单位

- **每个页面类型的活动单位** — 您最多可以为每个页面类型（主页、类别、产品详细信息、购物车、确认）创建50个活动推荐单位。 当达到限制时，创建流中的页面类型将灰显。
- **每单位的产品数** — 推荐单位中显示的产品数可以从5（默认值）设置为最多20。
- **草稿状态** — 将推荐保存为草稿后，将无法修改该单位的页面类型或推荐类型。 在激活之前，可以编辑其他设置。

## 过滤器和条件

- **动态条件** — 在除主页之外的每种页面类型上都可以使用动态条件（例如“与当前产品属于同一类别的产品”或“相对价格范围”）。 此外，它们还不可用于通过Page Builder放置推荐的页面。 查看[条件](filters.md#conditions)。

## 预览和非生产环境

- **最近查看过的预览** — 无法在管理员中预览&#x200B;_最近查看过的_&#x200B;推荐类型，因为该数据基于浏览器历史记录，在管理员上下文中不可用。 查看[预览推荐](create.md#preview)。
- **来自其他数据空间的推荐** — 当您[从非生产店面的其他SaaS数据空间](settings.md)（例如，生产环境）获取推荐时，您可以查看推荐，但无法从中单击进入产品页面。 这是专为预览和测试而设计的。
- **GraphQL和备用数据空间** — 通过[GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/)使用产品推荐时，`alternateEnvironmentId`参数（用于从其他数据空间获取推荐）不可用。 使用REST API或管理员设置在非生产环境中切换推荐源。

## API和配置

- **API密钥（4.x及更高版本）** — 您必须为沙盒和生产环境提供公共API密钥和私有API密钥。 如果您未提供这两对API密钥，则无法在管理员中访问产品推荐功能。 您店面上的数据收集和现有推荐将继续有效。 请参阅[安装和配置](install-configure.md)。

## Cookie限制

- 启用[Cookie限制模式](setting-cookie.md)且购物者未接受Cookie时，某些依赖行为数据的推荐类型可能不会显示或可能显示有限的结果。
- 启用Cookie限制后，不依赖行为数据的推荐类型（例如，_查看次数最多_、_视觉相似度_）继续工作。
- 启用Cookie限制后，在购物者同意之前，产品推荐不会在Cookie或本地存储中收集或存储行为数据。

## 页面生成器

- **量度和存储视图** - Page Builder推荐单位的量度仅显示在产品推荐工作区的默认存储视图中。 要在非默认商店视图上查看页面生成器推荐量度，您必须打开并[编辑](edit.md)该商店视图中的页面生成器推荐单元并保存它；然后将显示该商店视图的量度。 请参阅[页面生成器集成](page-builder.md)。

## B2B

- 产品推荐遵循[类别权限](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/categories/category-permissions.html)、[共享目录](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/shared-catalogs/catalog-shared.html)和特定于客户组的定价。 购物者只能根据自己的区段和目录分配看到他们能够访问的产品的推荐。 请参阅[入门](onboarding.md)。

## 数据和就绪性

- **行为数据** — 许多推荐类型需要足够的店面行为数据（视图、添加到购物车、购买）。 在收集到足够的数据之前，新存储区或低流量存储区可能会看到这些类型的结果有限或没有结果。 在管理员中监视[就绪指示器](create.md#readiness-indicators)。
- **不带生产数据的暂存** — 在没有行为数据的非生产环境中，您可以测试而不从生产中提取的唯一推荐类型是&#x200B;_更类似于_，它仅使用基于目录的相似度。 请参阅[暂存环境](staging-environment.md)。

## 故障排除

有关目录同步、建议未显示或其他常见问题的帮助，请搜索[Commerce知识库](https://experienceleague.adobe.com/zh-hans/docs/commerce-knowledge-base/kb/overview)或联系[支持部门](https://experienceleague.adobe.com/zh-hans/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide)。
