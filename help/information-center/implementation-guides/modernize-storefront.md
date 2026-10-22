---
title: 实现现有店面的现代化
description: 了解如何计划从旧版Adobe Commerce店面到基于Edge Delivery Services和插件构建的店面的增量迁移。
role: Developer, Leader
feature: Storefront
recommendations: noCatalog
autotag-review: '2026-10-20T11:09:14.812Z'
TQID: 'https://experienceleague.adobe.com/1OR7uwncjLw-NpwMMuwKjDjpASdh74sfu6s5rNClqxg'
product_v2:
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%
---

# 实现现有店面的现代化

您可以逐步将旧版店面迁移到Edge Delivery Services和Commerce下拉组件，而不是一次重建所有内容。

>[!NOTE]
>
>本指南适用于云基础架构上的Adobe Commerce as a Cloud Service、Adobe Commerce，或者使用Storefront Services或Adobe Commerce Optimizer Connector的内部部署。 它还适用于具有现有或第三方后端的独立Adobe Commerce Optimizer。 要确认哪个选项适用于您的项目，请参阅[实施架构选项](../architecture-options/implementation-architectures.md)。

## 快速入门

1. 要了解在Edge Delivery Services上构建的店面与您当前实施的比较，请查看[Adobe Commerce店面概述](https://experienceleague.adobe.com/en/tools/commerce-storefront/)。

1. 使用[Storefront Developer Guide](https://experienceleague.adobe.com/en/tools/commerce-storefront/get-started/)确定首先迁移哪些页面或流程。

1. 对于Adobe Commerce as a Cloud Service，请保留您现有的Commerce服务连接([!DNL Catalog Service]、[!DNL Live Search]、[!DNL Product Recommendations]、[!DNL Payment Services]) — 请参阅[设置Commerce服务](set-up-commerce-services.md)。

## 相关指导

- [新建店面](build-new-storefront.md)
- [架构选项](../architecture-options/overview.md)
