---
title: Store Fulfillment Services入门概述
description: '[!DNL Live Search]载入流程、系统要求、边界和限制。'
role: Admin, Leader
level: Intermediate
feature: Shipping/Delivery, Install
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---

# 商店功能的入门概述

通过设置、配置和启用以下组件开始使用[!DNL Store Fulfillment for Adobe Commerce by Walmart Commerce Technologies]：

- **Store Fulfillment扩展** — 在您的Adobe Commerce实例上安装并配置此第三方扩展。 安装后，您可以从管理员配置和管理Store Fulfillment解决方案，以支持Commerce店面中的[!DNL buys online, pickup in store] (BOPIS)方案。

  管理员视图中的![[!DNL Store Fulfillment Service]配置](assets/store-fulfillment-admin-home.png)

- **存储完成帐户** — 在启用过程中，客户经理将创建您的存储完成帐户，并向您提供帐户信息和凭据。 启用Adobe Commerce与“商店履行”解决方案之间的连接需要这些凭据。

- **Store Assist应用程序** — 为商店关联提供端到端商店履行工作流，以管理来自移动设备的BOPIS订单。 Store Associates可以下载并安装沃尔玛的[!DNL Store Assist]用于iOS和Android™设备。 应用程序载入流程由沃尔玛Commerce技术客户中心作为单独的流程进行管理。 但是，已经从Adobe Commerce管理员中完成[某些应用程序配置设置](user-setup.md)。

  | 商店协助应用程序 — 入门视图 | 应用商店助手应用程序 — 模块视图 |
  |-------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|
  | 在移动设备上查看![[!DNL Store Assist App Getting Started]](assets/store-assist-get-started-small.png) | 移动设备![&#128279;](assets/store-assist-orders-small.png)上的[!DNL Store Assist App Orders view] |

## 配置步骤

- **注册[!DNL Store Fulfillment for Adobe Commerce by Walmart Commerce Technologies]** — 完成[business.adobe.com](https://business.adobe.com/resources/store-fulfillment.html)上的注册表单，或联系您的Adobe Commerce客户经理寻求帮助。

- **启动存储履行配置请求** — 完成客户经理提供的接收表单，以提供开始配置过程所需的信息。

- **获取商店履行帐户凭据** — 在为您创建商店履行帐户后，您将收到将商店履行解决方案与Adobe Commerce集成所需的凭据。

- **[下载源代码以安装 [!DNL Store Fulfillment] 扩展](install.md)**

## 载入步骤

1. [安装Adobe Commerce的Store Fulfillment扩展](install.md)。

1. 从管理员[启用解决方案](enable-general.md)。

1. [从Adobe Commerce管理员配置Store Fulfillment扩展](service-config-settings-overview.md)。

1. [使用提供给您的“商店履行”凭据连接 [!DNL Store Fulfillment] 服务](connect-set-up-service.md)。

1. [为Store Assist应用创建用户和角色](user-setup.md)。

1. [将沃尔玛的 [!DNL Store Assist] 应用下载到您所需的设备。 该应用程序在Apple应用程序(iOS)和Google Play (Android™)](app-setup.md)商店中均可用。

在成功安装、配置、完成载入并访问[!DNL Store Assist]应用程序后，您可以[开始创建订单和测试](test-and-deploy.md)。
