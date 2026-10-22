---
title: 适用于Commerce的AEM Assets集成
description: 了解如何将AEM Assets与Adobe Commerce、Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer集成以集中管理产品图像和媒体。
role: Admin, Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T01:34:13.564Z'
TQID: 'https://experienceleague.adobe.com/v15DE37DoqpstrsWqnwd6DYpa5moT-BhQ80zDq2KP6I'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: ef0c45ae-6bee-4821-a65e-e1e118e8a01c
    internal-label: Commerce Optimizer
feature_v2:
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 4%
---

# 适用于Commerce的AEM Assets集成

AEM Assets集成启用了Adobe Commerce中的产品可视化功能，因此您可以在AEM Assets中集中管理产品图像、视频和其他媒体。 它是一个可选加载项，可与任何Commerce架构选项配合使用，而不是一个单独的Commerce平台。

## 按架构划分的集成路径

有两种集成路径。 具体路径取决于您的Commerce架构。

| Commerce架构 | AEM Assets集成路径 | 了解详情 |
| --- | --- | --- |
| 云或内部部署中的[!DNL Adobe Commerce] | Commerce的[!DNL AEM Assets]集成。 使用Commerce集成包同步和管理[!DNL Adobe Commerce]和[!DNL AEM Assets]之间的产品图像、视频和其他媒体。 | 适用于Commerce的[AEM Assets集成](/help/aem-assets-integration/overview.md) |
| [!DNL Adobe Commerce as a Cloud Service] | 由[!DNL AEM Assets]提供支持的[!DNL Product Visuals] | [AEM Assets集成设置](/help/aem-assets-integration/overview.md#next-steps) |
| 独立[!DNL Adobe Commerce Optimizer] | [!DNL Product Visuals]由[!DNL AEM Assets]提供支持。 基本目录和价格数据通过[Optimizer数据摄取API](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/)到达。 | 使用AEM Assets的[产品视觉效果](/help/optimizer/setup/product-visuals.md) |
| [!DNL Adobe Commerce]与[!DNL Adobe Commerce Optimizer Connector] | [!DNL Product Visuals]由[!DNL AEM Assets]提供支持。 目录和价格数据由Connector从[!DNL Adobe Commerce]同步。 | [Commerce Optimizer集成](/help/optimizer/integrations/integrations-overview.md) |

[!DNL Product Visuals]是Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer的集成路径。 它将AEM管理的产品图像同步到Commerce目录层，并通过店面API交付给店面体验。

## 选择之前

- 云上或本地路径与Commerce as a Cloud Service或Commerce Optimizer [!DNL Product Visuals]路径上的设置和许可要求不同。 首先查看特定于部署的要求。
- [!DNL AEM Assets]管理数字资源。 它不会替换Commerce catalog、pricing、cart、checkout或order system。
- 产品资源会使用SKU或其他记录的匹配元数据来与Commerce产品匹配。
- 如果营销和促销团队需要集中化的产品图像和资源工作流，请选择与您的Commerce架构匹配的路径。

## 相关信息

- [Adobe Experience Manager Assets文档](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/assets/overview)
- [架构概述](../architecture-options/overview.md)
- [API](../apis/commerce-apis.md)
