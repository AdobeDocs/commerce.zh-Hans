---
title: 信息源表架构参考
description: 了解 [!DNL Adobe Commerce Optimizer Connector] 用于跟踪馈送项目状态、导出状态和错误详细信息的馈送表架构。
autotag-review: '2026-06-23T00:00:00.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="仅限PaaS" type="Informative" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于云项目（Adobe管理的PaaS基础架构）和内部部署项目上的Adobe Commerce 。"
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 19de20caafd45e3a00896d0d4b29b7e96dfe94e1
workflow-type: tm+mt
source-wordcount: 324
ht-degree: 0%

---


# 馈送表架构参考

每个馈送在[!DNL Adobe Commerce]数据库中都有一个专用的MySQL表。 所有信息源表共享相同的列结构。

## 支持的源

有关受支持的带有API端点、批处理限制、索引器名称和馈送表名称的馈送的完整列表，请参阅[连接器模块和馈送端点](connector-reference.md#supported-feeds)。

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
| `status` | INT | 上次导出尝试后的提交状态代码。 请参阅[信息源提交和错误处理](../connector-sync-pipeline.md#feed-submission-and-error-handling)。 |
| `errors` | 文本 | 此项目的[!DNL Commerce Optimizer] API返回的JSON编码错误详细信息 |
| `metadata` | JSON | 导出框架使用的内部同步标志和锁定元数据信息 |

## 常见诊断查询

使用以下SQL查询直接检查馈送表状态。 `feed_data`列以[!DNL Adobe Commerce Optimizer] API格式存储数据。 将占位符值（如`<SKU>`、`<ATTRIBUTE_CODE>`、`<SLUG>`和`<PRICE_BOOK_ID>`）替换为环境中的实际值。

**产品信息源 — 按SKU：**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.sku') AS 'SKU',
       JSON_EXTRACT(f.feed_data, '$.source.locale') AS 'locale',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_products_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.sku') IN ('<SKU>');
```

**产品属性信息源 — 按属性代码：**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.code') AS 'code',
       JSON_EXTRACT(f.feed_data, '$.source.locale') AS 'locale',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_product_attributes_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.code') IN ('<ATTRIBUTE CODE>');
```

**类别信息源 — 按URL路径：**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.slug') AS 'slug',
    JSON_EXTRACT(f.feed_data, '$.source.locale') AS 'locale',
    f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_categories_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.slug') IN ('<SLUG>');
```

**价格信息源 — 按SKU：**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.sku') AS 'SKU',
       JSON_EXTRACT(f.feed_data, '$.priceBookId') AS 'price book ID',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_product_prices_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.sku') IN ('<SKU>');
```

**价格手册信息源 — 按价格手册ID：**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.priceBookId') AS 'price book ID',
    JSON_EXTRACT(f.feed_data, '$.name') AS 'name',
    JSON_EXTRACT(f.feed_data, '$.parentId') AS 'parent price book ID',
    JSON_EXTRACT(f.feed_data, '$.currency') AS 'currency',
    f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_price_books_feed f
WHERE JSON_UNQUOTE(JSON_EXTRACT(f.feed_data, '$.priceBookId'))  IN ('<PRICE_BOOK_ID>');
```

>[!MORELIKETHIS]
>
>- [连接器模块和馈送端点](connector-reference.md)
>- [连接器同步管道](../connector-sync-pipeline.md)
>- [管理同步](../data-sync-manage.md)
>- [连接器馈送的字段映射](field-mapping.md)
