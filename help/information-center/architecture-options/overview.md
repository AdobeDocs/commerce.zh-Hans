---
title: Commerce架构概述
description: 了解Adobe Commerce产品模型，以及在何处查找详细的架构选项、店面和API指南。
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T10:11:03.706Z'
TQID: 'https://experienceleague.adobe.com/V9Zp0eS8b45xYEay4EK91tPVnKhRdkWGDj4Vv7hB79U'
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
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
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
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: da3860b0-d637-47df-bef0-273751180266
    internal-label: Digital asset management
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%
---

# Commerce架构概述

Adobe Commerce架构通常将三个层组合在一起：商业后端（[!DNL Adobe Commerce]或[!DNL Adobe Commerce Optimizer]）、店面以及一组连接的服务和集成。 本部分将向您介绍产品模型，并介绍每个专用页面中维护的详细比较、图和API引用。

## 快速入门

| 部分 | 使用它可以 |
| ------- | --------- |
| [平台和服务](../portfolio/platform-and-services.md) | 了解每个Commerce产品是什么 — Adobe Commerce、Commerce Foundation、Adobe Commerce Optimizer和Adobe Commerce as a Cloud Service。 |
| [选择Commerce选项](../portfolio/choose-commerce-option.md) | 根据交易所有权、部署模型和促销需求比较Commerce选项。 |
| [架构选项](../architecture-options/implementation-architectures.md) | 详细比较所有四个受支持的体系结构，包括系统示意图和参考链接。 |
| [店面](../storefronts/overview.md) | 了解店面选项以及它们如何连接到每个体系结构。 |
| [API](../apis/commerce-apis.md) | 比较在Commerce Foundation、Storefront Services和Commerce Optimizer中使用的API系列。 |
| Commerce的[AEM Assets集成](../aem-assets/aem-assets-integration.md) | 将集中式数字资产管理添加到任何Commerce或Optimizer架构。 |
| [迁移和采用](../migration-adoption/overview.md) | 规划在体系结构之间迁移或分阶段采用Adobe Commerce Optimizer。 |

## 术语快速参考

| 首选术语 | 含义 | 避免使用作为当前架构标签 |
| --- | --- | --- |
| **Commerce Foundation** | 基本商业和事务性功能 | 核心Commerce和PHP基础层 |
| **店面服务** | 面向店面的API，用于目录服务、实时搜索和产品推荐 | 标签限制为仅一个Commerce平台 |
| **Commerce Optimizer促销服务** | 用于目录发现和促销体验的Optimizer API | Commerce Foundation API |
| 由Edge Delivery Services支持的&#x200B;**Commerce店面** | 面向客户的店面实施 | API系列 |

## 相关指导

- [实施体系结构](implementation-architectures.md)
- [参考体系结构](reference-architectures.md)
- [新建店面](../implementation-guides/build-new-storefront.md)
