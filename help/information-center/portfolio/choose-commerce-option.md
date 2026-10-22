---
title: 选择一个Commerce选项
description: 根据事务所有权、部署模型和销售需求比较Adobe Commerce体系结构。
role: Admin, Developer, Leader, User
feature: Storefront, Integration, Configuration
recommendations: noCatalog
TQID: 'https://experienceleague.adobe.com/5y0IU5nji50eqfFNQHbVDV-R81Mx0I8v5Y0a6nccL-w'
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
  - id: 22bad240-8308-569b-a9d5-578f1ff890ca
    internal-label: Customers
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 6388cf7b-8a81-5248-a1e4-7bb57bbe250f
    internal-label: Install
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
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
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: 4c3c267873a68560a885c6376cd1137a7503710a
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%
---

# 选择一个Commerce选项

首先确定哪个系统拥有购物车、结账、订单和其他交易。 然后，选择适合该后端的促销路径。

## 指导您决策的问题

使用以下问题来确定要评估的选项。 考虑您现有的商务后端，您希望保留多少基础架构责任，以及是否需要改进产品发现和推销。 Adobe Commerce Optimizer提供发现和促销功能。 它不会替换处理事务的后端。

1. **是否希望Adobe将Commerce平台作为软件即服务(SaaS)进行管理？**
   - 是：评估Adobe Commerce as a Cloud Service。
   - 否：如果您需要Adobe Commerce并且希望保留对云或本地基础架构的控制，请在云上或本地评估Adobe Commerce。
1. **您是否需要Adobe Commerce来处理购物车、结帐、订单和其他交易？**
   - 是：在云上或内部部署，或Adobe Commerce as a Cloud Service上评估Adobe Commerce。 这些选项使用Commerce Foundation作为事务性后端。
   - 否：保留现有或第三方事务型后端。 如果您还需要Adobe探索和促销功能，请评估独立的Adobe Commerce Optimizer。
1. **是否要使用Adobe Commerce Optimizer改进现有第三方商务后端的产品发现和商品促销？**
   - 是：评估独立的Adobe Commerce Optimizer，同时保留交易的第三方后端。
1. **您是否已在云中或内部部署运行Adobe Commerce，并希望进行更强大的发现和促销？**
   - 是：评估Adobe Commerce Optimizer连接器，以便在Adobe Commerce继续处理交易时同步目录和定价数据。

使用下面的比较表将您的答案与起点进行匹配。 有关详细的系统图，请参阅[架构选项](../architecture-options/overview.md)。

## 比较Commerce选项

| 您的要求 | 推荐的起点 | 拥有交易记录的系统 | 推销和发现 |
| --- | --- | --- | --- |
| Adobe以SaaS形式管理Commerce平台。 | [Adobe Commerce as a Cloud Service](/help/cloud-service/overview.md) | Adobe Commerce as a Cloud Service基础 | 使用为Adobe Commerce as a Cloud Service配置的Commerce服务。 有关Adobe Commerce Optimizer集成的可用性，请参阅此表下面的说明。 |
| 需要Adobe Commerce，并希望保留对云或内部部署基础架构的控制。 | 云或本地[Adobe Commerce](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/start/guide-overview) | Adobe Commerce Foundation | 根据需要使用支持的Commerce服务。 |
| 在Adobe Commerce上或内部部署，并希望采用Adobe Commerce Optimizer进行发现和促销。 | 具有[Adobe Commerce Optimizer Connector](/help/aco-connector/overview.md)的Adobe Commerce | Adobe Commerce仍然是交易的记录系统。 | 连接器将目录和定价数据同步到Adobe Commerce Optimizer，后者提供发现和促销体验。 |
| 具有一个第三方商业后端，并且希望在不替换该后端的情况下进行Adobe Commerce Optimizer发现和促销。 | 独立[Adobe Commerce Optimizer](/help/optimizer/overview.md) | 您的第三方商业后端 | 将目录和价格数据发送到Adobe Commerce Optimizer。 通过API Mesh、App Builder或直接集成，将购物车、结账和其他事务性操作与后端集成。 |

>[!NOTE]
>
>Adobe Commerce as a Cloud Service与Adobe Commerce Optimizer的集成位于Commerce路线图上。 如果您同时需要两个平台，请立即计划将它们用作单独的架构选项。 请联系您的Adobe客户经理以了解有关集成时间线的更多信息。

## 相关指导

- [平台和服务](platform-and-services.md)
- [架构选项](../architecture-options/overview.md)
- [快速入门](../get-started/get-started-by-role.md)
