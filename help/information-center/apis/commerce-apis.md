---
title: COMMERCE API
description: 比较Adobe Commerce API系列，包括Commerce Foundation、Storefront Services、Commerce Optimizer促销服务和数据摄取。
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T01:36:11.529Z'
TQID: 'https://experienceleague.adobe.com/JBpnpCy9QITdcYtKnL2btd9grmgIk1prYaCNasgWkok'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: ef0c45ae-6bee-4821-a65e-e1e118e8a01c
    internal-label: Commerce Optimizer
feature_v2:
  - id: 22bad240-8308-569b-a9d5-578f1ff890ca
    internal-label: Customers
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 72863f3c-9d27-5dda-afe1-d9f934b1fba0
    internal-label: Extensibility
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: c4f010fa-1478-4300-a88d-706fbc036a7a
    internal-label: APIs and SDKs
subfeature_v2:
  - id: e396cff5-f586-484c-89f0-7f1da3308f92
    internal-label: GraphQL
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: da3860b0-d637-47df-bef0-273751180266
    internal-label: Digital asset management
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%
---

# API

| API系列 | 主要目的 | 使用者 |
| --- | --- | --- |
| **Commerce Foundation GraphQL API** | 核心商务和事务型功能，如目录操作、购物车、结账、客户和订单 | 云上的[!DNL Adobe Commerce]、内部部署上的[!DNL Adobe Commerce]和[!DNL Adobe Commerce as a Cloud Service] |
| **Storefront Services GraphQL API** | 通过[!DNL Catalog Service]、[!DNL Live Search]和[!DNL Product Recommendations]面向店面的目录、搜索和推荐体验 | 云上或具有已配置服务的内部部署中的[!DNL Adobe Commerce]，以及[!DNL Adobe Commerce as a Cloud Service] |
| **Commerce Optimizer促销服务GraphQL API** | 检索Optimizer管理的目录、目录视图、价格上下文、搜索、推荐和促销结果 | 使用Optimizer Connector在云或内部部署的[!DNL Adobe Commerce]以及独立的[!DNL Adobe Commerce Optimizer] |
| **Commerce Optimizer数据摄取REST API** | 将目录和价格数据添加到独立的[!DNL Adobe Commerce Optimizer]实施 | 连接到外部数据源的单机[!DNL Adobe Commerce Optimizer] |

## Commerce Foundation GraphQL API

核心商务功能，包括目录、购物车、结账、客户和订单。 由[!DNL Adobe Commerce]在云中使用，[!DNL Adobe Commerce]在内部部署中使用，以及[!DNL Adobe Commerce as a Cloud Service]使用。 查看[Commerce GraphQL API](https://developer.adobe.com/commerce/webapi/graphql/)。

## Storefront Services GraphQL API

通过[!DNL Catalog Service]、[!DNL Live Search]和[!DNL Product Recommendations]面向店面的目录、搜索和推荐体验。 由[!DNL Adobe Commerce]在云、内部部署和[!DNL Adobe Commerce as a Cloud Service]上使用。 查看[Storefront Services GraphQL架构](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/)。

## Commerce Optimizer促销服务GraphQL API

检索Optimizer管理的目录、目录视图、价格上下文、搜索、推荐和促销结果。 由[!DNL Adobe Commerce]在云中使用、通过[!DNL Adobe Commerce Optimizer Connector]内部部署以及独立的[!DNL Adobe Commerce Optimizer]。 请参阅[Commerce Optimizer促销服务](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/)。

## Commerce Optimizer数据摄取REST API

将目录和价格数据从外部数据源添加到独立的[!DNL Adobe Commerce Optimizer]实施。 请参阅[Commerce Optimizer数据摄取](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/)。

## Commerce Optimizer集成

[!DNL Adobe Commerce Optimizer]通过多个集成路径连接到其他系统，具体取决于它是与[!DNL Adobe Commerce]配对还是与第三方后端配对。

### Adobe Commerce Optimizer连接器

将目录和价格数据从云或内部部署上的[!DNL Adobe Commerce]同步到[!DNL Adobe Commerce Optimizer]，将[!DNL Adobe Commerce]保留为交易系统，而Optimizer提供发现和促销。 请参阅[Commerce Optimizer集成](/help/optimizer/integrations/integrations-overview.md)。

### 第三方商业集成

通过数据摄取REST API将来自第三方商业平台、PIM、ERP或其他源的目录和价格数据摄取到独立的[!DNL Adobe Commerce Optimizer]，而第三方平台仍然是事务性记录系统。

### API Mesh和App Builder

使用API Mesh通过私有或第三方API编排Adobe Commerce API。 使用Adobe Developer App Builder构建自定义应用程序和集成。 有关相关的Commerce可扩展性指导，请参阅[API网格](https://developer.adobe.com/graphql-mesh-gateway/)和[Adobe Commerce可扩展性](https://developer.adobe.com/commerce/extensibility/)。

有关事件驱动的集成，请参阅[Adobe I/O Events for Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/extensibility/adobe-developer-app-builder/io-events/getting-started-io-events)。


### 购物车和结帐切换

对于具有外部后端的独立[!DNL Adobe Commerce Optimizer]，店面会使用Merchandising Services GraphQL API提供产品体验，然后通过API Mesh、App Builder或直接集成将购物车、结账、客户、订单、付款、税务、配送和履行服务交付到后端。

### AEM Assets

AEM Assets是一个可选的跨领域数字资产管理集成，可添加到任何Commerce或Optimizer架构，而不是其自身的单独集成路径。 查看Commerce的[AEM Assets集成](../aem-assets/aem-assets-integration.md)。

## 相关指导

- [架构概述](../architecture-options/overview.md)
- [店面](../storefronts/overview.md)
- [适用于Commerce的AEM Assets集成](../aem-assets/aem-assets-integration.md)
