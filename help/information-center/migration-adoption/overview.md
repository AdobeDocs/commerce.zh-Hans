---
title: 迁移和采用
description: 了解采用Adobe Commerce Optimizer、实现现有店面现代化或完全迁移到Adobe Commerce as a Cloud Service的途径。
role: Admin, Developer, Leader
feature: Storefront, Integration, Configuration
recommendations: noCatalog
TQID: 'https://experienceleague.adobe.com/2iEJ6fA-wLr18bi9C8l-w3srx1AWlAtiGt1cG9RPv0Q'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
feature_v2:
  - id: 1783ae9f-7157-5aeb-a915-91e260301e46
    internal-label: Routes
  - id: 22bad240-8308-569b-a9d5-578f1ff890ca
    internal-label: Customers
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 72863f3c-9d27-5dda-afe1-d9f934b1fba0
    internal-label: Extensibility
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: 4c3c267873a68560a885c6376cd1137a7503710a
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%
---

# 迁移和采用

采用无需进行单个、一次性的平台更改。 根据您的直接目标是店面现代化、促销改进、后端现代化还是完全迁移到托管软件即服务(SaaS)来选择路由。

## 采用途径

### 实现现有Adobe Commerce部署的现代化

- 将现有的Commerce Foundation保留为事务性后端。
- 采用由[!DNL Edge Delivery Services]提供支持的Commerce店面。
- 使用Storefront Services、App Builder、API Mesh和可选的AEM Assets集成。

### 使用Commerce Optimizer作为桥

- 使用[!DNL Adobe Commerce Optimizer Connector]连接[!DNL Adobe Commerce]云或内部部署。
- 采用促销服务、发现、推荐和Edge Delivery Services店面。
- 将[!DNL Adobe Commerce]保留为产品、价格、目录结构、购物车、结账、客户和订单的主要记录系统。
- 使用此架构作为向[!DNL Adobe Commerce as a Cloud Service]的可能过渡。

### 完全迁移到Adobe Commerce as a Cloud Service

- 评估当前的应用程序、自定义项、集成、店面以及数据。
- 使用与SaaS兼容的扩展性模式实现自定义项现代化。
- 重建或调整店面与集成。
- 迁移并验证目录、客户、订单、配置和受支持的自定义数据。
- 测试、切换并运行新的SaaS环境。

### 采用独立的Adobe Commerce Optimizer

- 从第三方Commerce平台、PIM、ERP或其他来源摄取目录和价格数据。
- 使用[!DNL Adobe Commerce Optimizer]促销服务进行目录检索、发现、推荐和促销。
- 使用由[!DNL Edge Delivery Services]提供支持的Commerce店面。
- 在连接的第三方系统中保留购物车、结账、客户、订单、付款、税务、配送和履行。

## 推荐的序列

1. 评估当前状态并定义系统所有权。
1. 建立API优先的集成边界。
1. 实现店面和体验层的现代化。
1. 同时采用促销服务和AEM Assets。
1. 根据需要迁移Commerce Foundation。
1. 验证、切换、监控和优化。

## 相关指导

- [选择一个Commerce选项](../portfolio/choose-commerce-option.md)
- [架构选项](../architecture-options/overview.md)
- [实现现有店面的现代化](../implementation-guides/modernize-storefront.md)
- [启用Adobe Commerce Optimizer](../implementation-guides/enable-aco.md)
