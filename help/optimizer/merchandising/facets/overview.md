---
title: Facet概述
description: 了解 [!DNL Adobe Commerce Optimizer] 中的Facet以及它们如何改进搜索结果。
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目(Adobe管理的SaaS基础架构)。"
exl-id: cf16626e-8f85-47ca-b973-891b16c31fe3
source-git-commit: b786a8675625dc969b9542b4b4f716de5342c1af
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 0%

---

# Facet

Facet是一种高性能筛选方法，它使用属性值的多个维度作为搜索条件。

![已过滤的搜索结果](../../assets/storefront-search-results-run.png)

在一个Facet中，购物者可以选择多个选项，例如“样式”下的“基本”和“紧靠”，搜索结果将更新以仅显示这些样式。 同样，如果购物者在多方面选择选项，例如“样式”下的“基本”和“气候”下的“室内”，则搜索结果会更新以显示所选样式和所选气候。

任何定义的Facet都可以用作URL参数，并将根据参数值过滤结果： `http://yourstore.com?brand=acme&color=red`。

## Facet聚合

按如下方式执行Facet聚合：如果店面具有三个Facet（类别、颜色和价格），并且购物者对所有三个（颜色=蓝色，价格为$10.00-50.00，类别= `promotions`）都进行过滤。

- `categories`聚合 — 聚合`categories`，然后应用`color`和`price`筛选器，但不应用`categories`筛选器。
- `color`聚合 — 聚合`color`，然后应用`price`和`categories`筛选器，但不应用`color`筛选器。
- `price`聚合 — 聚合`price`，然后应用`color`和`categories`筛选器，但不应用`price`筛选器。

## 默认属性值

以下产品属性由[!DNL Adobe Commerce Optimizer]使用并默认启用。

| 属性 | 描述 | 属性 |
|---|---|---|
| 可排序 | 用于产品列表中的排序 | `price` |
| 可搜索 | 在搜索中使用 | `price` <br />`sku`<br />`name` |

请参阅[数据摄取元数据API](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/#metadata)，了解有关产品属性及其属性的更多信息。

## 分层搜索和搜索类型扩展

分层搜索（即搜索内的搜索）是一种基于属性的过滤系统，它扩展了传统的搜索功能以包括附加搜索参数。 这些额外的搜索参数允许更精确、更灵活地发现产品。

通过分层搜索，您可以：

- 使购物者能够在搜索结果中进行搜索。
- 在分层搜索的第二层中使用`startsWith`和`contains`搜索索引来进一步优化结果。

高级搜索功能是使用特定运算符通过`filter`查询[`productSearch`中的](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/)参数实现的：

- **分层搜索** — 在另一个搜索上下文中搜索 — 使用此功能，您最多可以为搜索查询执行两层搜索。 例如：

   - **第1层搜索** — 在`product_attribute_1`上搜索“motor”。
   - **第2层搜索** — 在`product_attribute_2`上搜索“部件号123”。 此示例在结果中搜索“motor”的“部件号123”。

  分层搜索可用于分层搜索的第二层中的`startsWith`搜索索引和`contains`搜索索引，如下所述：

- **startsWith搜索索引** — 使用`startsWith`索引进行搜索。 此功能允许：

   - 搜索属性值以指定字符串开头的产品。
   - 配置“结尾为”搜索，以便购物者可以搜索属性值以特定字符串结尾的产品。
      - 要启用“结束于”搜索，需要反向摄取产品属性，并且API调用也应该是一个反向字符串。 例如，如果您要搜索以“pants”结尾的产品名称，则需要以“stnap”形式发送此项。

- **包含搜索索引** — 使用包含索引搜索属性。 此新功能允许：

   - 在较大的字符串中搜索查询。 例如，如果购物者搜索字符串“HAPE-123”中的产品编号“PE-123”。

      - 注意：此搜索类型不同于现有的[短语搜索](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#phrase)，后者执行自动完成搜索。 例如，如果您的产品属性值为“outdoor pants”，则短语搜索会返回“out pan”的响应，但不会返回“oor ants”的响应。 但是，包含搜索会返回“或蚂蚁”的响应。

这些新条件增强了搜索查询过滤机制以细化搜索结果。 这些新条件不会影响主搜索查询。

### 实现

1. [将属性设置为可搜索](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata)。

1. 指定该属性的搜索功能，如&#x200B;**Contains**（默认值）或&#x200B;**Starts with**。 您可以为&#x200B;**Contains**&#x200B;指定最多六个要启用的属性，为&#x200B;**Starts with**&#x200B;指定六个要启用的属性。 此外，对于&#x200B;**Contains**&#x200B;索引，字符串长度限制为50个字符或更少。

1. 有关如何使用新的[和](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-using-search-capability)搜索功能更新[!DNL Commerce Optimizer] API调用的示例，请参阅`contains`开发人员文档`startsWith`。

   您可以在搜索结果页面上实施这些新条件。 例如，您可以在页面上添加新部分，购物者可以进一步细化其搜索结果。 您可以允许购物者选择特定的产品属性，如“制造商”、“部件号”和“说明”。 从该位置，他们使用`contains`或`startsWith`条件在这些属性中搜索。

### 何时使用分层搜索而非Facet

分层搜索和Facet在产品发现中有不同的用途，它们之间的选择取决于您的特定用例：

**使用分层搜索：**

- 使用多个条件在搜索结果中搜索
- 使用用户了解部分信息的部件号、SKU或技术规范
- 允许购物者使用嵌套标准逐步缩小结果
- 通过在单个查询中组合多个搜索条件来减少API调用的数量
- 实施业务特定的搜索模式，这些模式不仅限于标准的分面导航

**使用Facet：**

- 提供典型类别、价格、品牌和属性过滤
- 提供用户可轻松理解和选择的直观筛选器选项
- 根据当前搜索结果显示可用选项
- 显示有助于用户了解可用选项的过滤器计数和范围
- 使用常见的产品特征，如颜色、尺寸、材质等

**最佳实践：**&#x200B;对于用户具有特定标准的复杂技术搜索，请使用分层搜索；对于用户希望直观地浏览和优化选项的标准电子商务筛选，请使用Facet。
