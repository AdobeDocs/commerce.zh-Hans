---
title: Facet
description: '[!DNL Live Search]个Facet使用属性值的多个维度作为搜索条件。'
exl-id: d036265e-1868-461d-ab4c-7f469b1c6f5b
source-git-commit: 269f68868f5df14b1ca3709c01f6c17e6775df05
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 0%

---

# Facet

分面是一种高性能筛选方法，它使用多个属性值的维度作为搜索条件。 分面搜索类似，但比标准[分层导航](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/navigation/navigation-layered.html?lang=zh-Hans)更“智能”。 可用筛选器的列表由搜索结果中返回的产品的[可筛选属性](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/navigation/navigation-layered.html?lang=zh-Hans#filterable-attributes)确定。

[!DNL Live Search]使用`productSearch`查询，该查询返回刻面和[!DNL Live Search]特有的其他数据。 有关代码示例，请参阅开发人员文档中的[`productSearch`查询](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/)。

![已过滤的搜索结果](assets/storefront-search-results-run.png)

在一个Facet中，购物者可以选择多个选项，例如“样式”下的“基本”和“紧靠”，搜索结果将更新以仅显示这些样式。 同样，如果购物者在多方面选择选项，例如“样式”下的“基本”和“气候”下的“室内”，则搜索结果会更新以显示所选样式和所选气候。

任何定义的Facet都可以用作URL参数，并将根据参数值过滤结果： `http://yourstore.com?brand=acme&color=red`。

## 彩块化要求

分面的类别和产品属性要求与用于分层导航的可过滤属性类似。 属性的每个店面属性必须将“在搜索结果中用于分层导航”值设置为“是”。 您可以从Admin中的[!DNL Stores] > [!DNL Attribute]菜单查看和更新属性配置。

>[!NOTE]
>
>如果将产品类别定义为Facet，则Facet将显示类别和子类别的`url_path`。
>
>![类别Facet](assets/facet-category.png)

请参阅[边界和限制](./boundaries-limits.md#facets)以了解有关[!DNL Live Search]中Facet要求的更多信息。

如果要与大量属性冲突，请考虑将属性组合到单个“meta-attribute”中。 例如，鞋的尺寸通常为数字，而衬衫的尺寸通常为“S/M/L/XL”。 这两种类型的大小可以合并为一个可搜索属性。

| 设置 | 描述 |
|--- |--- |
| [类别显示设置](https://experienceleague.adobe.com/docs/commerce-admin/catalog/categories/create/categories-display-settings.html?lang=zh-Hans) | 锚点 — `Yes` |
| [属性属性](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create.html?lang=zh-Hans) | [目录输入类型](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/attributes-input-types.html?lang=zh-Hans) - `Yes/No`、`Dropdown`、`Multiple Select`、`Price`、`Visual swatch`（仅限构件）、`Text swatch`（仅限构件） |
| 属性店面属性 | 在搜索结果分层导航中使用 — `Yes` |

## Facet聚合

按如下方式执行Facet聚合：如果店面具有三个Facet（类别、颜色和价格），并且购物者对所有三个（颜色=蓝色，价格为$10.00-50.00，类别= `promotions`）都进行过滤。

* `categories`聚合 — 聚合`categories`，然后应用`color`和`price`筛选器，但不应用`categories`筛选器。
* `color`聚合 — 聚合`color`，然后应用`price`和`categories`筛选器，但不应用`color`筛选器。
* `price`聚合 — 聚合`price`，然后应用`color`和`categories`筛选器，但不应用`price`筛选器。

## 默认属性值

以下产品属性具有[店面属性](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/product-attributes.html?lang=zh-Hans)，这些属性由[!DNL Live Search]使用并默认启用。

| 属性 | 店面属性 | 属性 |
|---|---|---|
| 可排序 | 用于产品列表中的排序 | `price` |
| 可搜索 | 在搜索中使用 | `price` <br />`sku`<br />`name` |
| FilterableInSearch | 在分层导航中使用 — 可过滤（包含结果） | `price`<br />`visibility`<br />`category_name` |

## 默认的非系统属性属性

下表显示了非系统属性的默认搜索和可过滤属性，包括那些特定于Luma示例数据的属性。 将&#x200B;*Use in Search*&#x200B;属性属性设置为`Yes`可使该属性在[!DNL Live Search]和本机Adobe Commerce中均可搜索。

| 属性代码 | 可搜索 | 在分层导航中使用 |
|--- |--- |--- |
| 活动 | 是 | 可筛选（包含结果） |
| attributes_brand | 是 | 否 |
| 品牌 | 是 | 否 |
| 气候 | 是 | 可筛选（包含结果） |
| 项圈 | 是 | 可筛选（包含结果） |
| 颜色 | 是 | 可筛选（包含结果） |
| 成本 | 是 | 否 |
| eco_collection | 是 | 可筛选（包含结果） |
| 性别 | 是 | 可筛选（包含结果） |
| 制造商 | 是 | 可筛选（包含结果） |
| 材料 | 是 | 可筛选（包含结果） |
| 用途 | 是 | 可筛选（包含结果） |
| 捆绑_包 | 是 | 可筛选（包含结果） |
| style_general | 是 | 可筛选（包含结果） |

## 默认系统属性属性

下表显示了系统属性的默认搜索和可过滤属性。

| 属性代码 | 可搜索 | 在分层导航中使用 |
|--- |--- |--- |
| allow_open_amou | 是 | 可筛选（包含结果） |
| 描述 | 是 | 否 |
| name | 是 | 否 |
| 价格 | 是 | 可筛选（包含结果） |
| short_description | 是 | 否 |
| sku | 是 | 否 |
| 状态 | 是 | 否 |
| tax_class_id | 是 | 否 |
| url_key | 是 | 否 |
| 粗细 | 是 | 否 |
