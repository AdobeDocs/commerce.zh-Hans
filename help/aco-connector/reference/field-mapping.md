---
title: '[!DNL Adobe Commerce Optimizer Connector]馈送的字段映射'
description: 了解从[!DNL Adobe Commerce]目录数据到所有馈送的[!DNL Adobe Commerce Optimizer]摄取API格式的[!DNL Adobe Commerce Optimizer Connector]字段映射。
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="仅限PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于云项目（Adobe管理的PaaS基础架构）和内部部署项目上的Adobe Commerce 。"
autotag-review: '2026-06-09T15:49:03.934Z'
TQID: 'https://experienceleague.adobe.com/SOWOnguudhqzX-r66nGUqc-WKet5qq6GRV11ADx0Me4'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
  - id: b23e006f-0a29-4f1d-8fd0-77aa56f3d12b
    internal-label: Data modeling
source-git-commit: 1e34df4f07f9043675104fce55c58e0617463b33
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 2%
---

# 连接器信息源的字段映射

本页记录了[!DNL Adobe Commerce Optimizer Connector]如何将[!DNL Adobe Commerce]目录字段转换为[!DNL Commerce Optimizer] [!DNL Catalog Data Ingestion API]所需的格式。 有关支持的馈送及其API端点的列表，请参阅[连接器引用](connector-reference.md#supported-feeds)。

## 产品

`products`馈送将数据发送到[Products终结点](https://developer.adobe.com/commerce/services/reference/rest/#tag/Products){target="_blank"}。

| [!DNL Adobe Commerce]字段 | [!DNL Commerce Optimizer] API字段 | 映射详细信息 |
| ----------------------------------------------- | -------------- | ------- |
| `sku` | `sku` | |
| `storeViewCode` | `source/locale` | |
| `name` | `name` | |
| `urlKey` | `slug` | |
| `productId` | `externalIds[0].id` | 将`origin`设置为`"AdobeCommerce"` |
| `status` | `status` | 将状态转换为大写。 如果状态缺失，或可配置或捆绑产品没有选项值，则使用`DISABLED`。 |
| `description` | `description` | 如果缺少描述，则使用空字符串。 |
| `shortDescription` | `shortDescription` | 如果缺少简短描述，则使用空字符串。 |
| `visibility` | `visibleIn` | 拆分逗号分隔值并将`Catalog`映射到`CATALOG`并将`Search`映射到`SEARCH`。 删除其他值。 |
| `metaTitle` | `metaTags/title` | |
| `metaDescription` | `metaTags/description` | |
| `metaKeyword` | `metaTags/keywords` | 将换行分隔的关键字拆分为数组，并修剪空格。 |
| `inStock`, `lowStock`, `weight`, `weightUnit` | `attributes[].code = "aco_ac_attributes"` | 始终添加`aco_ac_attributes`条目作为第一个属性。 其JSON值包含`inStock`和`lowStock`作为字符串。 当值可用时，它包含`weight`和`weightType`。 |
| `attributes[]` | `attributes[]` | 将每个条目映射到其属性代码、字符串值和匹配的变量引用ID（如果可用）。 跳过`inStock`、`lowStock`、`categories`、`weight`和`weightType`。 与库存相关的值包含在`aco_ac_attributes`中。 类别将导出为路由。 |
| `images[]` | `images[]` | 跳过没有URL的图像。<br>导出`url`、`label` （如果缺少则为空）和`sortOrder` （整数，默认为`0`）。<br>按`sortOrder`升序对图像进行排序。<br>将标准角色：`image`映射到`BASE`，`small_image`映射到`SMALL`，`thumbnail`映射到`THUMBNAIL`，`swatch_image`映射到`SWATCH`。 将其他角色导出为`customRoles[]`。 |
| `categoryData[].categoryPath` | `routes[].path` | 跳过类别路径为空的条目。 |
| `categoryData[].productPosition` | `routes[].position` | 如果缺少产品位置，则使用`0`。 |
| `links[].type` + `links[].sku` | `links[]` | `type`大写；已丢弃不含`sku`的条目 |
| `parents[].productType` + `parents[].sku` | `links[]` | 将`configurable`映射到`VARIANT_OF`，并将`bundle`或`bundle_fixed`映射到`IN_BUNDLE`。 将其他产品类型转换为大写。 跳过没有SKU的父母。 |
| `configurable options` | `configurations[]` | 导出具有ID和至少一个值的选项。<br>将`id`映射到`attributeCode`。 在`swatchType`存在时将`type`设置为`SWATCH`，否则设置为`CONFIGURABLE`。<br>使用默认值的ID作为`defaultVariantReferenceId`。<br>将每个值映射到`variantReferenceId`、`label`、`colorHex`和`imageUrl`。 |
| `bundle options` | `bundles[]` | 导出至少包含一个项目的选项。<br>使用选项标签作为`group`，如果标签为空，则使用`Bundle group`。 将`required`复制到输出。<br>将`checkbox`和`multi`渲染类型的`multiSelect`设置为`true`。<br>列出`defaultItemSkus`中的默认SKU。 每个项目包括`sku`、`qty`（默认为`0`）和`userDefinedQty`（从`qtyMutability`，默认为`false`）。 |

## 产品属性元数据

`productAttributes`馈送将数据发送到[元数据终结点](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata){target="_blank"}。

| [!DNL Adobe Commerce]字段 | [!DNL Commerce Optimizer] API字段 | 映射详细信息 |
| --------------- | -------------- | ------- |
| `attributeCode` | `code` | |
| `storeViewCode` | `source/locale` | |
| `label` | `label` | |
| `dataType` + `frontendInput` | `dataType` | 请参阅下面的转化表 |
| `dataType`和`frontendInput` | `dataType` | 使用以下转化规则。 |
| `visible`, `visibleInSearch`, `visibleInListing`, `visibleInCompareList` | `visibleIn[]` | 当标志为`true`时，将其对应的值添加：<br>`visible` → `PRODUCT_DETAIL`<br>`visibleInSearch` → `SEARCH_RESULTS`<br>`visibleInListing` → `PRODUCT_LISTING`<br>`visibleInCompareList` → `PRODUCT_COMPARE` |
| `filterable` | `filterable` | |
| `sortable` | `sortable` | |
| `searchable` | `searchable` | |
| `searchWeight` | `searchWeight` | |
| `searchTypes` | `searchTypes` | |

### 数据类型转换

当`dataType`为`int`时，连接器检查`frontendInput`。 对于其他数据类型，`frontendInput`不会影响转换。

| 输入`dataType` | 输入`frontendInput` | 输出`dataType` |
| ---------------- | --------------------- | ----------------- |
| `int` | `boolean` | `BOOLEAN` |
| `int` | `text`或`select` | `TEXT` |
| `int` | 任何其他值，包括缺少的值 | `INTEGER` |
| `decimal` | 未使用 | `DECIMAL` |
| `text`, `varchar`, `static`, `datetime` | 未使用 | `TEXT` |
| `OBJECT` | 未使用 | `OBJECT` |
| 任何其他值 | 未使用 | `TEXT` |

>[!NOTE]
>
>当属性使用`OBJECT`数据类型时，[产品API](https://developer.adobe.com/commerce/services/reference/graphql/#products){target="_blank"}尝试将其存储值解析为JSON。 如果解析成功，则API将返回值作为嵌套对象。 对于不能表示为单个值的结构化属性数据，请使用`OBJECT`。 有关说明，请参阅[动态添加产品属性](../../data-export/add-attribute-dynamically.md)。

## 价格手册

`priceBooks`信息源将数据发送到[价格手册终结点](https://developer.adobe.com/commerce/services/reference/rest/#tag/Price-Books){target="_blank"}。

与其他连接器馈送不同，[!DNL Adobe Commerce]中的[!DNL SaaS Data Export]索引器不收集`priceBooks`馈送。 连接器从管理员的网站和客户组配置生成此信息源。

对于每个网站，连接器会为每个客户组创建一个基本价格手册和一个子价格手册。

对`priceBookId`使用这些公式：

- 常规价格的基础价格手册： `priceBookId = websiteCode`。
- 客户组的子价格手册： `priceBookId = websiteCode::sha1(customerGroupId)`，其中`sha1(customerGroupId)`是客户组的整数ID的SHA-1十六进制摘要。

价格信息源使用相同的公式将每个价格条目分配给价格手册。 有关店面如何为客户会话解析`priceBookId`的信息，请参阅[Headless店面集成](../headless-storefront.md#graphql-commerceoptimizer-query)。


| Source字段或值 | [!DNL Commerce Optimizer] API字段 | 映射详细信息 |
| ---------------- | -------------- | ------- |
| `websiteCode` | `parentId` | 将此字段添加到子价格手册。 其值标识基本价格手册。 |
| 网站名称 | `name` | 使用基本价格手册的网站名称。 将`Customer group name (Website name)`用于子价格簿。 |
| `websiteCode` | `parentId` | 仅显示在子价格手册中；指向基本价格手册 |
| 网站基础货币 | `currency` | 仅包括基本价格手册上的此字段。 儿童价格手册省略了它。 |

## 价格

`prices`信息源将[!DNL Adobe Commerce]数据发送到[Prices终结点](https://developer.adobe.com/commerce/services/reference/rest/#tag/Prices){target="_blank"}。

| 馈送输入字段 | [!DNL Commerce Optimizer] API字段 | 映射详细信息 |
| --------------- | -------------- | ------------------------------------------------------------------------------- |
| `sku` | `sku` | 以不变方式传递SKU。 |
| `websiteCode`, `customerGroupCode` | `priceBookId` | 将`websiteCode`与`customerGroupCode`中客户组ID的SHA-1哈希合并。 如果`customerGroupCode`是`0`，则仅使用`websiteCode`。 |
| `regular` | `regular` | 以不变方式传递常规价格。 |
| `discounts[]` | `discounts[]` | 如果源值为`null`，则导出空数组。<br>对于将`code`设置为`special_price`并且值为`percentage`的条目，当值介于`0`和`100`之间时，将`percentage`设置为`100 - percentage`。 将该值设置为该范围内的`0`或该范围之外的值。<br>通过其他条目（包括基于价格的特殊价格），而不更改。 |
| `tierPrices[]` | `tierPrices[]` | 如果缺少源值或`null`，则使用空数组。 |

## 类别

`categories`源将[!DNL Adobe Commerce]数据发送到[类别终结点](https://developer.adobe.com/commerce/services/reference/rest/#tag/Categories){target="_blank"}。

将跳过具有空`urlPath`的项目（逻辑根类别），并且从不提交这些项目。

| [!DNL Adobe Commerce]字段 | [!DNL Commerce Optimizer] API字段 | 映射详细信息 |
| --------------- | -------------- | ------- |
| `storeViewCode` | `source/locale` | |
| `name` | `name` | |
| `urlPath` | `slug` | |
| `description` | `description` | |
| `position` | `position` | 导出类别位置（如果存在）。 当字段缺失时，忽略该字段。 |
| `metaTitle` | `metaTags/title` | |
| `metaDescription` | `metaTags/description` | |
| `metaKeywords` | `metaTags/keywords` | 新行分隔的字符串拆分为数组 |
| `image` | `images[].url` | 单元素数组；`roles: ["BASE"]` |
| `isActive` + `includeInMenu` | `families` | `["top_menu"]`，若两者均为`true`，否则`[]` |

| `metaKeywords` | `metaTags/keywords` |将换行分隔的关键字拆分到数组中并修剪空格。 |
| `image` | `images[].url` |当存在`image`时，将导出一个角色为`BASE`的图像。 在图像为空或缺少图像时导出空数组。 |
| `isActive` + `includeInMenu` | `families` |仅当两个值均为`true`时才添加`top_menu`。 否则，将导出空数组。 |
| `attributes[]` | `attributes[]` |将具有非空`attributeCode`的条目导出为`{code, values[]}`。 将值转换为字符串。 不存在符合条件的条目时省略`attributes`。 |

>[!MORELIKETHIS]
>
> - [使用数据摄取API摄取产品和价格数据](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/){target="_blank"} — 了解元数据、产品、类别、价格手册和价格的目录数据模型
> - [目录数据摄取REST API引用](https://developer.adobe.com/commerce/services/reference/rest/){target="_blank"} — 查看每个馈送端点的请求和响应架构
> - [如何与 [!DNL Commerce Optimizer Connector] 一起使用 [!DNL Adobe Commerce]](../overview.md#how-the-connector-works-with-adobe-commerce) — 了解商店查看次数、网站和客户组如何映射到目录源和价格手册
> - [价格手册位于 [!DNL Commerce Optimizer]](/help/optimizer/setup/pricebooks.md) — 管理连接器导出创建的价格手册
> - [Headless店面集成](../headless-storefront.md#graphql-commerceoptimizer-query) — 解决客户会话的`priceBookId`
