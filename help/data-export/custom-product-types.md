---
title: 在SaaS目录数据导出中支持自定义产品类型
description: 了解Commerce Storefront MCP目录启用模块如何使SaaS数据导出在发送到Live Search和目录服务的目录数据中表示无法识别的自定义第三方产品类型。
role: Admin, Developer
hide: true
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: d3cdead0-685a-4489-9250-4bb709942f66
    internal-label: Data collection
source-git-commit: fd87417a494987f33009d386019d870b306dcf73
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%
---
# 在SaaS目录数据导出中支持自定义产品类型

>[!IMPORTANT]
>
>作为[!DNL Commerce Storefront MCP]的一部分，对自定义产品类型的支持当前处于&#x200B;**早期访问**&#x200B;中。 Adobe Commerce版本2.4.4及更高版本支持此模块。 在正式发布之前，可用性、打包和安装要求可能会发生变化。 若要请求此&#x200B;**提前访问**&#x200B;的邀请，请发送电子邮件至[commerceeap@adobe.com](mailto:commerceeap@adobe.com)。 Adobe团队将通过后续步骤和资格要求做出响应。

## 概述

[!DNL SaaS Data Export]在为连接的Adobe Commerce服务（如[实时搜索](../live-search/overview.md)和[目录服务](../catalog-service/overview.md)）准备目录数据时，可识别标准Commerce产品类型（简单、可配置、捆绑包等）。 第三方扩展可以引入[!DNL SaaS Data Export]本身无法识别的&#x200B;**自定义产品类型**。

Commerce Storefront MCP目录启用模块允许[!DNL SaaS Data Export]在出站目录有效负荷中将这些无法识别的自定义产品类型表示为&#x200B;**简单产品**，因此使用[!DNL Commerce Storefront MCP]的购物者可以通过目录支持的服务发现它们。

## 行为的范围

- Commerce店面MCP目录启用模块不会更改Adobe Commerce中存储的产品类型。 将自定义产品类型表示为简单产品仅适用于发送到[!DNL Live Search]和[!DNL Catalog Service]的目录数据。
- 不需要管理员设置或运行时配置。 标准产品类型可继续正常导出。
- 此模块面向的是第三方扩展引入的自定义产品类型，而不是标准Commerce产品类型。

## 安装模块

要启用Commerce Storefront MCP目录启用模块，请从命令行运行以下命令：

```bash
composer require magento/module-storefront-mcp-enablement --no-update
composer update magento/module-storefront-mcp-enablement --with-dependencies
bin/magento setup:upgrade
```

## 重新同步您的目录数据

安装该模块不会更改Adobe Commerce中的基础产品数据，因此不会自动重新导出现有的自定义产品类型项目。 要将新的简单产品呈现应用于安装模块之前已同步的目录数据，请手动重新同步目录数据。 请参阅[手动重新同步数据](data-sync-manage.md#manually-resync-data)。
