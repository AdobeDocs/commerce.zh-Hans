---
title: Facet概述
description: 了解 [!DNL Adobe Commerce Optimizer] 中的Facet以及它们如何改进搜索结果。
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目(Adobe管理的SaaS基础架构)。"
exl-id: cf16626e-8f85-47ca-b973-891b16c31fe3
source-git-commit: ad8fb7d1d7e1ad124647ba84377079dcfbd46a3c
workflow-type: tm+mt
source-wordcount: '338'
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

## 默认的非系统属性属性

下表显示了非系统属性的默认搜索和可过滤属性。 将&#x200B;*Use in Search*&#x200B;属性属性设置为`Yes`可使该属性在[!DNL Adobe Commerce Optimizer]中可搜索。

| 属性代码 | 可搜索 |
|--- |--- |
| 活动 | 是 |
| attributes_brand | 是 |
| 品牌 | 是 |
| 气候 | 是 |
| 项圈 | 是 |
| 颜色 | 是 |
| 成本 | 是 |
| eco_collection |
| 性别 | 是 |
| 制造商 | 是 |
| 材料 | 是 |
| 用途 | 是 |
| 捆绑_包 | 是 |
| style_general | 是 |

## 默认系统属性属性

下表显示了系统属性的默认搜索和可过滤属性。

| 属性代码 | 可搜索 |
|--- |--- |
| allow_open_amou | 是 |
| 描述 | 是 |
| name | 是 |
| 价格 | 是 |
| short_description | 是 |
| sku | 是 |
| 状态 | 是 |
| tax_class_id | 是 |
| url_key | 是 |
| 粗细 | 是 |
