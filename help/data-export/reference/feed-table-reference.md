---
title: 信息源表架构参考
description: 了解 [!DNL SaaS Data Export] 用于跟踪馈送项目状态、导出状态和错误详细信息的馈送表架构。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Services
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: c70c1643afbf8e9633df89a613d6798416c8eb44
workflow-type: tm+mt
source-wordcount: 429
ht-degree: 0%

---


# 馈送表架构参考

每个馈送在[!DNL Adobe Commerce]数据库中都有一个专用的MySQL表。 所有信息源表共享相同的列结构。 下表列出了每个馈送及其CLI馈送名称、索引器ID和馈送表名称。

## 支持的源

馈送的实际列表取决于已安装的[!DNL SaaS Data Export]包。


| 信息源(`--feed`) | 用途 | 索引器ID | 信息源表 | 导出模式 |
| --- | ------------------------------------------------------------------- | --- | --- | --- |
| `products` | 产品目录（属性、类别、图像等） | `catalog_data_exporter_products` | `cde_products_feed` | 立即 |
| `productAttributes` | 属性定义和元数据。 用于定义搜索架构。 | `catalog_data_exporter_product_attributes` | `cde_product_attributes_feed` | 立即 |
| `categories` | 类别数据 | `catalog_data_exporter_categories` | `cde_categories_feed` | 立即 |
| `prices` | 产品价格与客户组价格和层价格 | `catalog_data_exporter_product_prices` | `cde_product_prices_feed` | 立即 |
| `variants` | 可配置的产品变体 | `catalog_data_exporter_product_variants` | `cde_product_variants_feed` | 立即 |
| `scopesWebsite` | 具有商店视图代码的网站 | `scopes_website_data_exporter` | `scopes_website_data_exporter` | 旧版 |
| `scopesCustomerGroup` | 客户组定义 | `scopes_customergroup_data_exporter` | `scopes_customergroup_data_exporter` | 旧版 |
| `productOverrides` | 计算的产品权限 | `catalog_data_exporter_product_overrides` | `cde_product_overrides_feed` | 立即 |
| `categoryPermissions` *(EE)* | 原始类别权限数据 | `catalog_data_exporter_category_permissions` | `cde_category_permissions_feed` | 立即 |
| `orders` | 销售订单状态 | `sales_order_data_exporter_v2` | `sales_data_exporter_orders_v2` | 旧版 |

**导出模式**&#x200B;列指示每个馈送收集和提交数据的方式：

- **立即模式馈送** — 收集数据，使用内容散列（哈希去重）跳过未更改的项目，并在同一索引器运行中提交更新。
- **旧模式馈送** (`scopesWebsite`， `scopesCustomerGroup`， `orders`) — 首先将组合的数据存储在馈送表中，并通过单独的cron作业提交它。

请参阅[同步模式](../sync-overview.md#synchronization-modes)。

## 架构

| 列 | 类型 | 描述 |
| --- | --- | ---------------- |
| `id` | 整数(PK) | 自动递增主键 |
| `source_entity_id` | INT | Commerce源表中的实体ID（例如，`catalog_product_entity.entity_id`） |
| `feed_id` | VARCHAR | 信息源项目的唯一标识符。 计算为项标识字段（例如，`sku + storeViewCode`）的哈希，而不是自动递增值。 |
| `feed_data` | JSON | 此项目的信息源有效负荷。 仅填充实体标识符和范围的最小信息。 当设置`PERSIST_EXPORTED_FEED=1`时，将存储完整有效负载。 |
| `feed_hash` | VARCHAR | 用于更改检测的内容哈希。 从有效负载进行计算，不包括时间戳(`modifiedAt`， `updatedAt`)。 如果哈希与上一次导出匹配，则不会重新提交该项目。 |
| `is_deleted` | TINYINT | 软删除标记。 在Commerce中删除实体时设置为`1`。 |
| `modified_at` | 时间戳 | 上次修改此信息源项目的时间 |
| `status` | INT | 上次导出尝试后的提交状态代码。 请参阅[信息源提交和HTTP错误处理](../sync-overview.md#feed-submission-and-http-error-handling)。 |
| `errors` | 文本 | SaaS服务为此项目返回的JSON编码错误详细信息 |
| `metadata` | JSON | 导出框架使用的内部同步标志和锁定元数据信息 |

## 常见诊断查询

使用以下SQL查询直接检查馈送表状态。 将占位符值（如`<SKU>`、`<ATTRIBUTE_CODE>`和`<CATEGORY_ID>`）替换为环境中的实际值。 有关表名的完整列表，请参阅[支持的源](#supported-feeds)。

**产品信息源 — 按SKU：**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.sku') AS 'SKU',
       JSON_EXTRACT(f.feed_data, '$.storeViewCode') AS 'store view code',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_products_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.sku') IN ('<SKU>');
```

**产品属性信息源 — 按属性代码：**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.attributeCode') AS 'code',
       JSON_EXTRACT(f.feed_data, '$.storeViewCode') AS 'store view code',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_product_attributes_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.attributeCode') IN ('<ATTRIBUTE_CODE>');
```

**价格信息源 — 按SKU：**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.sku') AS 'SKU',
       JSON_EXTRACT(f.feed_data, '$.websiteCode') AS 'website code',
       JSON_EXTRACT(f.feed_data, '$.customerGroupCode') AS 'customer group code',
       IFNULL(cg.customer_group_code, '-- (base price)') AS 'AC customer group',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_product_prices_feed f
LEFT JOIN customer_group cg
       ON sha1(cg.customer_group_id) = JSON_EXTRACT(f.feed_data, '$.customerGroupCode')
WHERE JSON_EXTRACT(f.feed_data, '$.sku') IN ('<SKU>');
```

**产品覆盖信息源 — 按SKU：**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.sku') AS 'SKU',
       JSON_EXTRACT(f.feed_data, '$.websiteCode') AS 'website code',
       JSON_EXTRACT(f.feed_data, '$.customerGroupCode') AS 'customer group code',
       IFNULL(cg.customer_group_code, 'NA (deleted)') AS 'AC customer group',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_product_overrides_feed f
LEFT JOIN customer_group cg
       ON sha1(cg.customer_group_id) = JSON_EXTRACT(f.feed_data, '$.customerGroupCode')
WHERE JSON_EXTRACT(f.feed_data, '$.sku') IN ('<SKU>');
```

**类别信息源 — 按类别ID：**

```sql
SELECT JSON_EXTRACT(feed_data, '$.categoryId') AS 'Category ID',
       JSON_EXTRACT(f.feed_data, '$.storeViewCode') AS 'store view code',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_categories_feed f
WHERE JSON_EXTRACT(feed_data, '$.categoryId') IN (<CATEGORY_ID>);
```

**变体馈送 — 按可配置的产品SKU：**

```sql
SELECT JSON_EXTRACT(feed_data, '$.parentSku') AS 'configurable SKU',
       JSON_EXTRACT(feed_data, '$.productSku') AS 'Variant SKU',
       JSON_EXTRACT(f.feed_data, '$.optionValues') AS 'options',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_product_variants_feed f
WHERE JSON_EXTRACT(feed_data, '$.parentSku') = '<SKU>';
```


>[!MORELIKETHIS]
>
>- [将数据与SaaS数据导出同步](../sync-overview.md)
>- [查看和管理同步](../data-sync-manage.md)
>- [使用Commerce CLI同步源](../data-export-cli-commands.md)
