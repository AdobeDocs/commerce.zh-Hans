---
title: '[!DNL Adobe Commerce Optimizer Connector]模块和信息源端点'
description: 了解 [!DNL Adobe Commerce]的 [!DNL Adobe Commerce Optimizer Connector] 模块、目录馈送API端点、批次限制和core_config_data配置路径。
feature: Integration, Configuration
badgePaas: label="仅限PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于云项目（Adobe管理的PaaS基础架构）和内部部署项目上的Adobe Commerce 。"
autotag-review: '2026-06-09T15:48:19.494Z'
TQID: 'https://experienceleague.adobe.com/UM6Y-xoQpUDzWpaMe1GRPp4XoAtHBLBsHw388kumN8g'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 296
ht-degree: 1%

---

# 连接器模块和馈送端点

此参考列出了`core_config_data`中存储的[!DNL Adobe Commerce Optimizer Connector]模块包、支持的馈送API端点和配置密钥路径。 要了解这些组件在同步期间如何协同工作，请参阅[连接器同步管道](../connector-sync-pipeline.md)。

## 模块

连接器包含多个Magento模块，这些模块收集目录数据，将馈送数据映射到[!DNL Commerce Optimizer] API支持的格式，并管理提交和范围控制。 下表总结了每个模块及其角色。

| 模块 | 角色 |
| ------ | ---- |
| `DataExporterAdapter` | 将[!DNL Adobe Commerce]源映射到[!DNL Adobe Commerce Optimizer] API所需的格式。 覆盖信息源池和架构配置。 |
| `SaasExportAdapter` | 将[!DNL Commerce Optimizer]馈送路由到摄取API，并阻止提交不支持的馈送。 |
| `CommerceAcoExporter` | 管理[!DNL Commerce Optimizer]凭据并提供CLI设置命令 |
| `CommerceAdapter` | [!DNL Commerce Optimizer] API兼容性层（GraphQL、捆绑包添加到购物车、配置UI） |
| `PriceBookDataExporter` | 按网站和客户组编制索引的价格手册信息源 |
| `SaasPriceBook` | 用于价格手册提交的SaaS基础架构 |
| `CommerceOptimizerScopeMapper` | 每个网站和每个商店视图同步启用 |

## 支持的源

连接器向[!DNL Commerce Optimizer] [[!DNL Catalog Data Ingestion API]](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/){target="_blank"}提交多个馈送类型。 下表列出了每个馈送及其在[!DNL Adobe Commerce]中的终结点、批处理限制、索引器名称和馈送表。

| 信息源 | [!DNL Commerce Optimizer] API终结点 | 批次限制 | AC索引名称 | 信息源表 |
| ---- | ----------------------------------- | ----------- | ------------- | ---------- |
| `products` | `POST /v1/catalog/products` | 100 | `catalog_data_exporter_products` | `cde_products_feed` |
| `categories` | `POST /v1/catalog/categories` | 100 | `catalog_data_exporter_categories` | `cde_categories_feed` |
| `productAttributes` | `POST /v1/catalog/products/metadata` | 100 | `catalog_data_exporter_product_attributes` | `cde_product_attributes_feed` |
| `prices` | `POST /v1/catalog/products/prices` | 500 | `catalog_data_exporter_product_prices` | `cde_product_prices_feed` |
| `priceBooks` | `POST /v1/catalog/price-books` | 500 | `data_exporter_price_books` | `cde_price_books_feed` |

`products`、`productAttributes`、`categories`和`prices`馈送重复使用[!DNL SaaS Data Export]索引器收集的数据。 连接器从网站和客户组配置生成`priceBooks`源，并且不依赖于[!DNL SaaS Data Export]索引器。

有关每个馈送的字段级映射详细信息，请参阅 [!DNL Commerce Optimizer Connector] 馈送[&#128279;](field-mapping.md)的字段映射。
若要根据目录大小估算同步所需的时间，请参阅[估算数据量和同步时间](estimate-data-volume-sync-time.md)。

## 配置路径

[!DNL Commerce Optimizer Connector]凭据和服务URL存储在`aco_exporter/general/`路径前缀下的`core_config_data`中。 运行`bin/magento aco:config:show`以查看当前值。 该命令不显示客户端密码。

```text
aco_exporter/general/org_id
aco_exporter/general/tenant_id
aco_exporter/general/client_id
aco_exporter/general/client_secret       (encrypted)
aco_exporter/general/type
aco_exporter/general/ingestion_url
aco_exporter/general/optimizer_studio_url
```
