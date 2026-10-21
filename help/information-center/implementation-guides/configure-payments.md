---
title: 配置付款
description: 了解如何为Adobe Commerce配置支付服务，以支持多种支付方式以及用于支付、订单和发票的统一仪表板。
role: Admin, Developer
feature: Configuration
recommendations: noCatalog
autotag-review: '2026-10-20T11:00:28.278Z'
TQID: 'https://experienceleague.adobe.com/egM9HoywqOQgL27ykw5SBdvoMHsmagYNoDMtNSLPds0'
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
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 591c578b-908e-5b79-a9d3-931dfe60c24c
    internal-label: Invoices
  - id: 6388cf7b-8a81-5248-a1e4-7bb57bbe250f
    internal-label: Install
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%
---

# 配置付款

[!DNL Payment Services]为购物者提供了多种支付方式（包括免息分期付款），并为商家提供了一个统一的控制面板来管理付款、订单和发票。

>[!NOTE]
>
>本指南适用于Adobe Commerce（云或本地）、Adobe Commerce as a Cloud Service或Magento Open Source处理事务的情况。 对于Adobe Commerce Optimizer项目，仅当事务性后端是这些受支持的平台之一时，才遵循此流程。 如果第三方后端处理事务，请改用后端的付款设置。

## 快速入门

1. 检查[付款服务兼容性](https://experienceleague.adobe.com/en/docs/commerce/payment-services/compatibility)中的产品版本和国家/地区可用性。

1. 遵循[载入支付服务流程](/help/payment-services/onboard.md)。

1. 如果您的Commerce on Cloud或内部部署实例未连接到Commerce Services，请首先执行[设置Commerce服务](set-up-commerce-services.md)。

## 相关指导

- [Payment Services指南概述](/help/payment-services/guide-overview.md)
- [设置Commerce服务](set-up-commerce-services.md)
