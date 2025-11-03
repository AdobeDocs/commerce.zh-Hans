---
title: 设置Live Search
description: ' [!DNL Live Search] 工作区用于配置、管理和监视搜索性能。'
exl-id: 07c32b26-3fa4-4fae-afba-8a10866857c3
source-git-commit: a22a57f52503811a3a3e9294174a6626c5630b79
workflow-type: tm+mt
source-wordcount: '1990'
ht-degree: 0%

---

# 设置Live Search

在工作区中，您可以配置、管理和监视[!DNL Live Search]的性能。 顶部的菜单提供对各个功能区域中工具的访问。 可用功能反映当前的菜单选择。

![Workspace](assets/workspace.png)

## 数据收集

要确保工作区上的每个功能区域都包含正确的数据，您需要根据选定的店面实施配置数据收集：

1. Luma — 数据收集现成可用。
1. Headless — 根据店面实施，必须手动配置数据收集。

如果您使用的是Headless店面，请参阅以下文档以获得有关需要添加的事件的更多信息：

- 实时搜索仪表板的[必需事件](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#live-search)。
- 需要添加为先决条件的[店面事件收集器](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/)。
- 事件结构的[示例](https://github.com/adobe/commerce-events/tree/main/examples)。

### 医疗保健客户

如果您是医疗保健客户，并且安装了[数据服务HIPAA扩展](../data-connection/hipaa-readiness.md#installation)（它是[数据连接](../data-connection/overview.md)扩展的一部分），则不再捕获[!DNL Live Search]使用的店面事件数据。 这是因为店面事件数据是在客户端生成的。 要继续捕获和发送店面事件数据，请为[!DNL Live Search]重新启用事件收集。 有关详细信息，请参阅[常规配置](https://experienceleague.adobe.com/en/docs/commerce-admin/config/general/general#data-services)。

## 设置范围

最初，所有[设置的](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html#scope-settings)作用域[!DNL Live Search]设置为`Default Store View`。 如果[!DNL Commerce]安装包含多个商店视图，请将&#x200B;**范围**&#x200B;设置为应用Facet设置的[商店视图](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html)。

## 菜单选项

| 选项 | 描述 |
|--- |--- |
| [性能](performance.md) | 功能板提供了用于了解产品搜索性能的insight。 |
| [彩块化](facets.md) | 高性能筛选，它使用属性值的多个维度来优化搜索条件。 |
| [同义词](synonyms.md) | 扩展搜索范围，以包含购物者可能用于查找与您的目录中的产品不同的字词。 |
| [搜索促销](rules.md) | 使用触发计划操作的逻辑规则塑造搜索体验。 提升、隐藏、固定或隐藏产品以校准搜索结果来支持您的业务目标。 |
| [类别促销](category-merch.md) | 在类别级别应用规则和智能促销。 |
| [GraphQL](graphql.md) | 登录到商店管理员的开发人员可以使用实际目录数据编写和测试查询。 要了解更多信息，请转到[开发人员文档中的](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/)GraphQL概述[!DNL Live Search]。 |
| [设置](settings.md) | 确定如何在店面中按价格范围对价格方面值进行分组并设置索引语言。 |

## 将属性设置为可搜索

要生成目标明确的结果，请查看[可搜索](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/product-attributes.html) (`searchable=true`)产品属性集。 为确保相关性，请仅在属性包含含义清晰而简洁的内容时才允许搜索属性。 避免使用包含不太精确、长度较长的文本的属性，例如`description`，虽然默认情况下启用了搜索，但可能会降低搜索结果的精度。 例如，如果人员搜索“短裤”，并且有描述包含“短袖”一词的衬衫，则衬衫将包含在搜索结果中。

要允许搜索属性，请完成以下步骤：

1. 在管理员中，转到&#x200B;**商店** > *属性* > **产品**。
1. 选择要可搜索的属性，如`color`。
1. 选择&#x200B;**店面属性**&#x200B;并将&#x200B;**在搜索中使用**&#x200B;设置为`yes`。

[!DNL Live Search]还遵循在Adobe Commerce中设置的产品属性的[权重](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search-results.html#weighted-search)。 权重较高的属性在搜索结果中的显示位置将较高。

以下属性始终可搜索：

- `sku`
- `name`
- `categories`

### 分层搜索和搜索类型扩展

分层搜索（即搜索内的搜索）是一种功能强大、基于属性的过滤系统，它扩展了传统的搜索功能，以包含额外的搜索参数。 这些额外的搜索参数允许更精确、更灵活地发现产品。

>[!NOTE]
>
>分层搜索在Live Search 4.6.0中可用。

通过分层搜索，您可以：

- 使购物者能够在搜索结果中进行搜索。
- 在分层搜索的第二层中使用`startsWith`和`contains`搜索索引来进一步优化结果。

高级搜索功能是使用特定运算符通过`filter`查询[`productSearch`中的](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/)参数实现的：

- **分层搜索** — 在另一个搜索上下文中搜索 — 使用此功能，您最多可以为搜索查询执行两层搜索。 例如：

   - **第1层搜索** — 在`product_attribute_1`上搜索“motor”。
   - **第2层搜索** — 在`product_attribute_2`上搜索“部件号123”。 此示例在结果中搜索“motor”的“部件号123”。

  分层搜索可用于分层搜索的第二层中的`startsWith`搜索索引和`contains`搜索索引，如下所述：

- **startsWith搜索索引** — 使用`startsWith`索引进行搜索。 此新功能允许：

   - 搜索属性值以指定字符串开头的产品。
   - 配置“结尾为”搜索，以便购物者可以搜索属性值以特定字符串结尾的产品。 要启用“结束于”搜索，需要反向摄取产品属性，并且API调用也应该是一个反向字符串。 例如，如果您要搜索以“pants”结尾的产品名称，则需要以“stnap”形式发送此项。

- **包含搜索索引** — 使用包含索引搜索属性。 此新功能允许：

   - 在较大的字符串中搜索查询。 例如，如果购物者搜索字符串“HAPE-123”中的产品编号“PE-123”。

      - 注意：此搜索类型不同于现有的[短语搜索](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#phrase)，后者执行自动完成搜索。 例如，如果您的产品属性值为“outdoor pants”，则短语搜索会返回“out pan”的响应，但不会返回“oor ants”的响应。 但是，包含搜索会返回“或蚂蚁”的响应。

这些新条件增强了搜索查询过滤机制以细化搜索结果。 这些新条件不会影响主搜索查询。

#### 实现

1. 在管理员中，[将产品属性](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/product-attributes-add#step-5-describe-the-storefront-properties)设置为可搜索。

   查看可搜索的[属性](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/attributes-input-types)的列表。

1. 指定该属性的搜索功能，如&#x200B;**Contains**（默认值）或&#x200B;**Starts with**。 您最多可以为&#x200B;**Contains**&#x200B;指定6个要启用的属性，为&#x200B;**Starts with**&#x200B;指定6个要启用的属性。 此外，对于&#x200B;**Contains**&#x200B;索引，字符串长度限制为50个字符或更少。

   ![指定搜索功能](./assets/search-filters-admin.png)

1. 有关如何使用新的[和](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-using-search-capability)搜索功能更新[!DNL Live Search] API调用的示例，请参阅`contains`开发人员文档`startsWith`。

   您可以在搜索结果页面上实施这些新条件。 例如，您可以在页面上添加新部分，购物者可以进一步细化其搜索结果。 您可以允许购物者选择特定的产品属性，如“制造商”、“部件号”和“说明”。 从该位置，他们使用`contains`或`startsWith`条件在这些属性中搜索。

### 何时使用分层搜索而非Facet

分层搜索和Facet在产品发现中有不同的用途，它们之间的选择取决于您的特定用例：

**在以下情况下使用分层搜索：**

- 您需要使用多个条件在搜索结果中进行搜索。
- 使用用户了解部分信息的部件号、SKU或技术规范。
- 购物者需要使用嵌套标准逐步缩小结果范围。
- 您希望通过在单个查询中组合多个搜索条件来减少API调用的数量。
- 您需要实施特定于业务的搜索模式，这些模式应超出标准彩块化导航的范围。

**在以下情况下使用Facet：**

- 提供典型类别、价格、品牌和属性过滤
- 提供用户可轻松理解和选择的直观过滤器选项
- 根据当前搜索结果显示可用选项
- 显示有助于用户了解可用选项的过滤器计数和范围
- 使用常见的产品特征，如颜色、尺寸、材质等。

**最佳实践：**&#x200B;对于用户具有特定条件的复杂技术搜索，使用分层搜索；对于用户希望直观地浏览和缩小选项范围的标准电子商务筛选，使用Facet。

## Facet和同义词

刻面和同义词是另一种增强购物者搜索体验的方式。

[Facet](facets.md)是[!DNL Live Search]中定义的可筛选的产品属性。 您可以在[!DNL Live Search]中将任何可筛选的属性设置为Facet，但您一次可以搜索的Facet数量存在[限制](boundaries-limits.md)。

>[!NOTE]
>
>仅当产品属性配置具有必需的属性时，才能筛选产品属性： *在搜索中使用=是*、*在搜索结果中使用分层导航=是*&#x200B;和&#x200B;*在分层导航中使用=可筛选（包含结果）*。 如果这些属性缺失或未正确设置，则该属性在Facet配置中不可见。 有关配置说明，请参阅[添加方面](facets-add.md#add-a-facet)。

[同义词](synonyms.md)是可以定义的术语，可帮助引导用户使用正确的产品。 寻找裤子的用户可能会输入“裤子”或“长裤”。 您可以设置同义词，以便这些搜索词将用户引进“裤子”结果。

## Commerce配置设置

以下部分介绍了[!DNL Live Search]支持和不支持的Commerce配置设置。

### 支持的配置值

>[!IMPORTANT]
>
>强烈建议您使用在Live Search 4.0.0中默认启用的产品列表小组件。这些小组件旨在完全取代未来版本中的适配器实施。 请参阅[启用产品列表小组件](install.md#enable-product-listing-widgets)以了解详情。

| Commerce配置设置 | 描述 | 受Popover支持 | 适配器支持 |
|---|---|---|---|
| 存储>配置>目录>目录>目录搜索>允许每页所有产品 | 如果设置为`Yes`，则在“每页显示”控件中包含`ALL`选项。 | 是的。 最多500个产品 | 是的。 最多500个产品 |
| 存储>配置>目录>目录>目录搜索>最小查询长度 | 目录搜索中允许的最小字符数。 | 是 | 是 |
| 存储>配置>目录>目录>目录搜索>每页产品在网格中的允许值 | 确定在网格视图中显示的产品数。 | 是 | 是 |
| 存储>配置>目录>目录>目录搜索>每页产品在网格上的默认值 | 确定网格视图中默认每页显示的产品数。 | 是的。 最多500个产品 | 是的。 最多500个产品 |
| 商店>配置>目录>库存>显示缺货产品 | 显示缺货的产品。 | 是 | 是 |
| 存储>配置>货币>默认显示货币 | 用于显示价格的主要货币。 | 是 | 是 |
| 存储>配置>常规>货币设置>货币选项>基本货币 | 用于所有联机付款交易记录的主要币种。 | 是 | 是 |

小组件产品列表页面和弹出框中的价格将使用配置的汇率转换为默认显示货币。

### 不支持的配置值

| Commerce配置设置 | 描述 | 注释 |
|---|---|---|
| 存储>配置>目录>店面>列表模式 | 确定搜索结果列表的格式。 | 正确呈现，但是对于某些页面交互，不会发送事件 |
| 存储>配置>目录>目录>目录搜索>最大查询长度 | 目录搜索中允许的最大字符数。 | 未实现；搜索服务最多接受255个字符 |
| 配置>销售>税>价格显示设置>在目录中显示产品价格 | 确定目录中所发布的产品价格是包含税还是不包含税，或显示两个版本价格；一个包含税，另一个不含税 |  |
| 商店>配置>目录>店面>产品列表排序依据 | 确定搜索结果列表的排序顺序。 | 不适用于[!DNL Live Search] [产品列表页小组件](plp-styling.md) |

## 默认属性值

以下产品属性具有[店面属性](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/product-attributes.html)，这些属性由[!DNL Live Search]使用并默认启用。

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
