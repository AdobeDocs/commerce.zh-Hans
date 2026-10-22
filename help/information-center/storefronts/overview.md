---
title: 店面
description: 了解Adobe Commerce店面选项，包括由Edge Delivery Services提供支持的Commerce店面和自定义Headless实施。
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T01:12:22.967Z'
TQID: 'https://experienceleague.adobe.com/1mQm2s3UGzr7S4j9RMZAaRoUVtzu93N1IFbOypR8vkA'
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
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
subfeature_v2:
  - id: e396cff5-f586-484c-89f0-7f1da3308f92
    internal-label: GraphQL
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%
---

# 店面

店面与Commerce后端和API层分开。 根据所选架构，店面可以通过API Mesh、App Builder或其他集成机制从Commerce Foundation API、Storefront Services API、[!DNL Adobe Commerce Optimizer]促销服务API或连接的系统中检索数据。 请参阅[架构选项](../architecture-options/overview.md)，了解每个店面如何与Commerce后端配对。

## 由Edge Delivery Services提供支持的Commerce店面

由[!DNL Edge Delivery Services]提供支持的Commerce店面是基于Adobe Commerce样板构建的面向客户的店面选项，使用插入组件和内容块。 它与任何[架构概述](../architecture-options/overview.md)兼容，可连接到Commerce Foundation、Storefront Services或[!DNL Adobe Commerce Optimizer]促销服务（具体取决于后端）。 查看[Adobe Commerce店面概述](https://experienceleague.adobe.com/en/tools/commerce-storefront/)。

## 店面服务

[!DNL Storefront Services]是与[!DNL Adobe Commerce]一起使用的面向店面的服务。 服务API提供了对以下功能的优化访问：

- [!DNL Catalog Service]
- [!DNL Live Search]
- [!DNL Product Recommendations]

云或本地（配置后）上的[!DNL Adobe Commerce]和[!DNL Adobe Commerce as a Cloud Service]都使用Storefront服务。 它们不专属于[!DNL Adobe Commerce as a Cloud Service]，不应用作两个[!DNL Adobe Commerce]平台选项之间的区别标签。 查看[Storefront Services GraphQL架构](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/)。

## 自定义Headless店面

在由[!DNL Edge Delivery Services]提供支持的Commerce店面之外的店面选项包括[!DNL Luma]、[!DNL PWA Studio]或自定义Headless店面，具体取决于平台支持和实施要求。 自定义Headless店面与任何其他店面选项（Commerce Foundation、Storefront Services或Commerce Optimizer Merchandising Services）连接到相同的API系列，具体取决于所选的[架构选项](../architecture-options/overview.md)。

## 购物车和结账集成

处理购物车和结账事务的位置取决于Commerce后端，而不是店面技术：

- 当[!DNL Adobe Commerce] Commerce Foundation是后端时，店面使用Commerce Foundation API进行购物车、结账、客户和订单操作，以及配置的付款、税务、配送和履行集成。
- 当第三方商务平台作为后端（与独立的[!DNL Adobe Commerce Optimizer]一样）时，店面通过API Mesh、App Builder或直接集成连接到该平台的购物车、结账、客户、订单、付款、税务、配送和履行服务。

## 相关指导

- [架构概述](../architecture-options/overview.md)
- [API](../apis/commerce-apis.md)
