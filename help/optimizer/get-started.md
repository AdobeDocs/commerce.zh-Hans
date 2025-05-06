---
title: 开始使用 [!DNL Adobe Commerce Optimizer]
description: 了解如何使用 [!DNL Adobe Commerce Optimizer]。
hide: true
recommendations: noCatalog
exl-id: de57d93d-e156-45c1-86aa-de29a8c34bd2
source-git-commit: ac79c8aa43ced017743fbef1f181b4eaf8e0a754
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---

# 开始使用

>[!NOTE]
>
>本文档描述了早期访问开发中的产品，并未反映用于正式发布的所有功能。

本指南将指导您完成创建和使用[!DNL Adobe Commerce Optimizer]实例。

<!--Click the tabs below to see high-level workflow overviews for the following user types:

- Administrators
- Merchants
- Developers

>[!BEGINTABS]

>[!TAB Administrator and merchant workflow]

This diagram provides a high-level overview of how administrators and merchants access and manage [!DNL Adobe Commerce Optimizer] instances. See the [Adobe Admin Console Guide](https://helpx.adobe.com/cn/enterprise/admin-guide.html) for more information about administrator workflows.

NEED DIAGRAM

>[!TAB Developer workflow]

This diagram provides a high-level overview of how developers create integrations for [!DNL Adobe Commerce Optimizer] using App Builder. See the [API documentation](https://developer.adobe.com/commerce/services/cloud/) for more information.

NEED DIAGRAM

>[!ENDTABS]
-->

## 配置

在[!DNL Adobe Commerce Optimizer]实例准备就绪后，[!DNL Adobe Commerce Optimizer]配置团队将为您提供以下端点：

| 项目 | 示例URL | 用途 |
|---|---|---|
| [!DNL Adobe Commerce Optimizer] UI | `https://experience.adobe.com/#/@commerceprojectbeacon/commerce-optimizer-studio?tenant=<tenantId>` | 访问Commerce Optimizer UI以跨以下项管理您的目录：<br>1。 促销规则（产品发现、产品推荐）。<br>2。 目录管理（渠道和策略创建）。<br>3。 数据分析（查看您的目录数据摄取状态）。 |
| 店面API | `https://na1-sandbox.api.commerce.adobe.com/<tenantId>/graphql` | 访问设置由Edge Delivery Services提供支持的Commerce店面所需的API。 |
| 目录数据摄取API | `https://na1-sandbox.api.commerce.adobe.com/<tenantId>/v1/catalog/<entity>` | 访问摄取目录数据所需的API。 |

>[!NOTE]
>
>请参阅[开发人员文档](https://developer-stage.adobe.com/commerce/services/composable-catalog/)，详细了解店面设置和目录摄取所需的API。

作为抢先体验参与者，您将收到一封包含安全链接的电子邮件，该链接与您的IMS令牌一起允许您登录[!DNL Adobe Commerce Optimizer]或进行API调用。

## 设置店面

现在您已经拥有[!DNL Adobe Commerce Optimizer]实例，您可以继续[设置](./storefront.md)由Edge Delivery Services支持的Commerce店面。

## 适用于早期访问参与者的可用目录数据

作为早期访问参与者，[!DNL Adobe Commerce Optimizer]实例包含基于[Carvelo用例](./use-case/admin-use-case.md)的模拟目录数据。 模拟数据以及一些预配置的渠道和策略可帮助您熟悉[!DNL Adobe Commerce Optimizer] UI。

<!--Ingest catalog data

By default, [!DNL Adobe Commerce Optimizer] instances do not include any product data.

See the [Ingestion API](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/using-the-api/) documentation to learn how you can import your catalog data into [!DNL Adobe Commerce Optimizer].

The catalog data that you ingest is visible in the [data insights](./insights-overview.md) page. Additionally, you can use the [Catalog](./catalog-overview.md) page to define the channels and policies.-->
