---
title: ' [!DNL Adobe Commerce Optimizer Connector] 馈送的字段映射'
description: 了解从 [!DNL Adobe Commerce] 目录数据到所有馈送的 [!DNL Adobe Commerce Optimizer] 摄取API格式的 [!DNL Adobe Commerce Optimizer Connector] 字段映射。
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="仅限PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于云项目（Adobe管理的PaaS基础架构）和内部部署项目上的Adobe Commerce 。"
autotag-review: '2026-06-09T15:49:03.934Z'
TQID: 'https://experienceleague.adobe.com/SOWOnguudhqzX-r66nGUqc-WKet5qq6GRV11ADx0Me4'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: e7dae43f-215c-4cdf-90d3-c5a461a6e669id: c32adafa-ed01-4b31-997e-2413013911b0
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: e0eb8757-182f-49f3-94a4-1587d16f5094id: b23e006f-0a29-4f1d-8fd0-77aa56f3d12b
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 665
ht-degree: 0%

---


# 连接器信息源的字段映射

本页记录了[!DNL Adobe Commerce Optimizer Connector]如何将[!DNL Adobe Commerce]目录字段转换为[!DNL Commerce Optimizer] [!DNL Catalog Data Ingestion API]所需的格式。 有关支持的馈送及其API端点的列表，请参阅[连接器引用](connector-reference.md#supported-feeds)。

## 产品

`products`馈送将数据发送到[Products终结点](https://developer.adobe.com/commerce/services/reference/rest/#tag/Products){target="_blank"}。

| [!DNL Adobe Commerce]字段 | [!DNL Commerce Optimizer] API字段 | 注释 |
| ----------------------------------------------- | -------------- | ------- |
| `sku` | `sku` | |
| `storeViewCode` | `source/locale` | |
| `name` | `name` | |
| `urlKey` | `slug` | |
| `productId` | `externalIds[0].id` | `origin`已修复到`"AdobeCommerce"` |
| `status` | `status` | 大写；对于未分配子项的复合产品，设置为`DISABLED` |
| `description` | `description` | |
| `shortDescription` | `shortDescription` | |
| `visibility` | `visibleIn` | 以逗号分隔的值拆分并映射： `Catalog`→`CATALOG`， `Search`→`SEARCH`；已丢弃未映射的值 |
| `metaTitle` | `metaTags/title` | |
| `metaDescription` | `metaTags/description` | |
| `metaKeyword` | `metaTags/keywords` | 新行分隔的字符串拆分为数组 |
| `inStock`, `lowStock`, `weight`, `weightUnit` | `attributes[].code = "aco_ac_attributes"` | JSON编码对象`{inStock, lowStock, weight, weightType}`；始终作为第一个属性条目存在 |
| `attributes[]` | `attributes[]` | 已排除映射到`{code, values[], variantReferenceId}`；`inStock`、`lowStock`、`weight`、`weightType`的每个条目（它们进入`aco_ac_attributes`） |
| `images[]` | `images[]` | `url`，`label`；映射的标准角色： `image`→`BASE`，`small_image`→`SMALL`，`thumbnail`→`THUMBNAIL`，`swatch_image`→`SWATCH`；非标准角色转至`customRoles[]` |
| `categoryData[].categoryPath` | `routes[].path` | |
| `categoryData[].productPosition` | `routes[].position` | |
| `links[].type` + `links[].sku` | `links[]` | `type`大写；已丢弃不含`sku`的条目 |
| `parents[].productType` + `parents[].sku` | `links[]` | 映射的类型： `configurable`→`VARIANT_OF`，`bundle`/`bundle_fixed`→`IN_BUNDLE` |
| `configurable options` | `configurations[]` | `id`→`attributeCode`，`label`；设置`swatchType`时选项类型`SWATCH`，否则`CONFIGURABLE`；默认变体来自`isDefault`；值包括`variantReferenceId`，`label`，`colorHex`，`imageUrl` |
| `bundle options` | `bundles[]` | `label`→`group`；`required`；`renderType` `checkbox`/`multi`→`multiSelect: true`；来自`isDefault`的默认SKU；项目包括`sku`、`qty`、`userDefinedQty` (`qtyMutability`) |

## 产品属性元数据

`productAttributes`馈送将数据发送到[元数据终结点](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata){target="_blank"}。


| [!DNL Adobe Commerce]字段 | [!DNL Commerce Optimizer] API字段 | 注释 |
| --------------- | -------------- | ------- |
| `attributeCode` | `code` | |
| `storeViewCode` | `source/locale` | |
| `label` | `label` | |
| `dataType` + `frontendInput` | `dataType` | 请参阅下面的转化表 |
| `visible` | `visibleIn: "PRODUCT_DETAIL"` | `true`时添加到数组 |
| `visibleInSearch` | `visibleIn: "SEARCH_RESULTS"` | `true`时添加到数组 |
| `visibleInListing` | `visibleIn: "PRODUCT_LISTING"` | `true`时添加到数组 |
| `visibleInCompareList` | `visibleIn: "PRODUCT_COMPARE"` | `true`时添加到数组 |
| `filterable` | `filterable` | |
| `sortable` | `sortable` | |
| `searchable` | `searchable` | |
| `searchWeight` | `searchWeight` | |
| `searchTypes` | `searchTypes` | |

### 数据类型转换

连接器从上述映射表中的Commerce `dataType`和`frontendInput`字段派生API `dataType`。 下表显示了连接器应用的转换规则。

| [!DNL Adobe Commerce] `dataType` | [!DNL Adobe Commerce] `frontendInput` | [!DNL Commerce Optimizer] API `dataType` |
| -------------------- | -------------------------- | ------------------- |
| `int` | `boolean` | `BOOLEAN` |
| `int` | `text`或`select` | `TEXT` |
| `int` | 任何其他 | `INTEGER` |
| `decimal` | - | `DECIMAL` |
| `text`, `varchar`, `static`, `datetime` | - | `TEXT` |
| `OBJECT` | - | `OBJECT` |
| 任何其他 | - | `TEXT` |

>[!NOTE]
>
>当属性的`dataType`设置为`OBJECT`时，[products API](https://developer.adobe.com/commerce/services/reference/graphql/#products){target="_blank"}将该属性值视为结构化对象而不是纯字符串。 在查询时，API尝试将存储的值解析为JSON。 如果解析成功，则结果将作为响应中的嵌套对象返回。 **当您动态提供自定义属性时（例如，用于承载不能表示为标量值的结构化或多字段数据），此行为特别有用**。 有关说明，请参阅[动态添加产品属性](../../data-export/add-attribute-dynamically.md)。

## 价格手册

`priceBooks`信息源将数据发送到[价格手册终结点](https://developer.adobe.com/commerce/services/reference/rest/#tag/Price-Books){target="_blank"}。

与其他连接器馈送不同，[!DNL Adobe Commerce]中的[!DNL SaaS Data Export]索引器不收集`priceBooks`馈送。 连接器从管理员的网站和客户组配置生成此信息源。

每个网站创建一个&#x200B;**基本价格手册**，另外每个网站 — 客户组对创建一个&#x200B;**子价格手册**。

**价格簿ID公式：**

- **基数**（正常价格）： `priceBookId = websiteCode`
- **子**（客户组或共享目录）： `priceBookId = websiteCode::sha1(customerGroupId)`，其中`sha1(customerGroupId)`是客户组的整数ID的SHA-1十六进制摘要

在解决价格条目所属的价格手册时，价格馈送使用相同的公式。 有关店面如何为客户会话解析`priceBookId`，请参阅[Headless店面集成](../headless-storefront.md#graphql-commerceoptimizer-query)。

| 生成的字段 | [!DNL Commerce Optimizer] API字段 | 注释 |
| ---------------- | -------------- | ------- |
| `websiteCode`, `customerGroupId` | `priceBookId` | |
| 网站名称 | `name` | 基本价格手册：网站名称。 子项： `"Group Name (Website Name)"` |
| `websiteCode` | `parentId` | 仅显示在子价格手册中；指向基本价格手册 |
| 网站基础货币 | `currency` | 仅存在于基础价格手册中；由子代继承 |

## 价格

`prices`信息源向[Prices终结点](https://developer.adobe.com/commerce/services/reference/rest/#tag/Prices){target="_blank"}发送数据。

| [!DNL Adobe Commerce]字段 | [!DNL Commerce Optimizer] API字段 | 注释 |
| --------------- | -------------- | ------------------------------------------------------------------------------- |
| `sku` | `sku` | |
| `websiteCode`, `customerGroupId` | `priceBookId` | |
| `regular` | `regular` | |
| `discounts[]` | `discounts[]` | 折扣示例：特殊价格、目录规则价格、共享目录价格 |
| `tierPrices[]` | `tierPrices[]` | |

## 类别

`categories`馈送将数据发送到[类别终结点](https://developer.adobe.com/commerce/services/reference/rest/#tag/Categories){target="_blank"}。

将跳过具有空`urlPath`的项目（逻辑根类别），并且从不提交这些项目。

| [!DNL Adobe Commerce]字段 | [!DNL Commerce Optimizer] API字段 | 注释 |
| --------------- | -------------- | ------- |
| `storeViewCode` | `source/locale` | |
| `name` | `name` | |
| `urlPath` | `slug` | |
| `description` | `description` | |
| `metaTitle` | `metaTags/title` | |
| `metaDescription` | `metaTags/description` | |
| `metaKeywords` | `metaTags/keywords` | 新行分隔的字符串拆分为数组 |
| `image` | `images[].url` | 单元素数组；`roles: ["BASE"]` |
| `isActive` + `includeInMenu` | `families` | `["top_menu"]`，若两者均为`true`，否则`[]` |

>[!MORELIKETHIS]
>
> - [使用数据摄取API摄取产品和价格数据](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/){target="_blank"} — 了解元数据、产品、类别、价格手册和价格的目录数据模型
> - [目录数据摄取REST API引用](https://developer.adobe.com/commerce/services/reference/rest/){target="_blank"} — 查看每个馈送端点的请求和响应架构
> - [如何与 [!DNL Commerce Optimizer Connector] 一起使用 [!DNL Adobe Commerce]](../overview.md#how-the-connector-works-with-adobe-commerce) — 了解商店查看次数、网站和客户组如何映射到目录源和价格手册
> - [价格手册位于 [!DNL Commerce Optimizer]](/help/optimizer/setup/pricebooks.md) — 管理连接器导出创建的价格手册
> - [Headless店面集成](../headless-storefront.md#graphql-commerceoptimizer-query) — 解决客户会话的`priceBookId`
