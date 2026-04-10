---
title: 发行说明
description: ' [!DNL Adobe Commerce Optimizer]的最新发行信息。'
role: Admin, Developer, User, Leader
recommendations: noCatalog
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和 [!DNL Adobe Commerce Optimizer] 项目（Adobe管理的SaaS基础架构）。"
exl-id: e420d461-9ea2-4e32-aa37-230b14a297d7
source-git-commit: d0967674d05018f13dc6c8a562005d65d44e42ab
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---

# 发行说明

以下发行说明包含[!DNL Adobe Commerce Optimizer]的更新。

## 2026年4月

**发行日期**：2026年4月7日

>[!BEGINSHADEBOX]

### 目录规则

销售规则现在包含[类别规则](./merchandising/rules/add.md)，因此您可以使用与搜索相同的智能排名和手动操作（固定、提升、嵌入）来定位一个或多个类别并控制类别页面上的产品订单。

### 价格筛选器

推荐筛选器现在支持[价格筛选器](./merchandising/recommendations/filters.md#price)，您可以使用该筛选器设置产品的最低和最高价格范围。

### 其他发行说明

[!DNL Adobe Commerce Optimizer]使用最新版本的AEM Assets集成、Commerce Optimizer连接器和[!DNL Adobe Commerce Storefront]。 请使用以下链接查看每个区域的发行说明：

| 可扩展性 | 店面 |
| --- | --- |
| [AEM Assets集成](../aem-assets-integration/release-notes.md)<br>[Commerce Optimizer连接器](../aco-connector/release-notes.md) | [店面版本信息](https://experienceleague.adobe.com/developer/commerce/storefront/releases/)<br>[店面变更日志](https://experienceleague.adobe.com/developer/commerce/storefront/releases/changelog/) |

>[!ENDSHADEBOX]

## 2026年2月

**发行日期**：2026年2月19日

>[!BEGINSHADEBOX]

添加了在[创建推荐单位](./merchandising/recommendations/create.md)或[促销规则](./merchandising/rules/add.md)时指定目录视图的功能。

### 其他发行说明

[!DNL Adobe Commerce Optimizer]使用最新版本的AEM Assets集成、Commerce Optimizer连接器和[!DNL Adobe Commerce Storefront]。 请使用以下链接查看每个区域的发行说明：

| 可扩展性 | 店面 |
| --- | --- |
| [AEM Assets集成](../aem-assets-integration/release-notes.md)<br>[Commerce Optimizer连接器](../aco-connector/release-notes.md) | [店面版本信息](https://experienceleague.adobe.com/developer/commerce/storefront/releases/)<br>[店面变更日志](https://experienceleague.adobe.com/developer/commerce/storefront/releases/changelog/) |

>[!ENDSHADEBOX]

## 2025年12月

**发行日期**：2025年12月10日

>[!BEGINSHADEBOX]

### 机会

AI支持的站点优化建议现在可通过[Adobe Sites Optimizer集成](./manage-results/opportunities.md)使用。 此功能通过自动检测和智能推荐，帮助商家识别并解决影响商业网站性能的问题。

### 目录层

添加了[目录层](./setup/catalog-layer.md)，以便您可以在不更改源数据的情况下修改产品数据，包括层优先级管理以及与Adobe Sites Optimizer自动修复功能的集成。

### 其他发行说明

[!DNL Adobe Commerce Optimizer]使用最新版本的AEM Assets集成、Commerce Optimizer连接器和[!DNL Adobe Commerce Storefront]。 请使用以下链接查看每个区域的发行说明：

| 可扩展性 | 店面 |
| --- | --- |
| [AEM Assets集成](../aem-assets-integration/release-notes.md)<br>[Commerce Optimizer连接器](../aco-connector/release-notes.md) | [店面版本信息](https://experienceleague.adobe.com/developer/commerce/storefront/releases/)<br>[店面变更日志](https://experienceleague.adobe.com/developer/commerce/storefront/releases/changelog/) |

>[!ENDSHADEBOX]

## 2025年10

**发行日期**：2025年10月14日

>[!BEGINSHADEBOX]

### Commerce Optimizer Salesforce Commerce连接器

[!DNL Commerce Optimizer Salesforce Commerce Connector]是一个新的App Builder集成入门工具包，它使Commerce管理员和开发人员能够将Salesforce B2C Commerce目录数据与[!DNL Commerce Optimizer]无缝连接。<!--COMOPT-536-->

管理员的&#x200B;**：**

* Salesforce中的目录更新（产品、价格、元数据、价格手册）会自动与Commerce Optimizer同步，无需手动干预。
* 该集成独立于Adobe Commerce运行，降低了复杂性和潜在的故障点。
* 管理员可以依赖计划的定期计划更新，以确保Commerce Optimizer中的目录数据准确无误，从而改进推介和产品推荐。

面向开发人员的&#x200B;**：**

* 入门套件提供了一个简单的、可扩展的框架，用于将Salesforce目录数据摄取到SaaS促销服务中。
* 提供了参考实施、设计文档和代码示例以加速自定义集成或疑难解答。<!--COMOPT-536-->

### 分层搜索

* 下列高级搜索功能的GA版本：使用`startsWith`和`contains`的分层搜索。 [了解详情](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#layered-search-and-expansion-of-search-types)。

### 类别API

新的类别REST API现已可用，它允许管理员和开发人员以编程方式创建、更新和管理多个类别树，以便导航和产品分组。 该API支持全局和特定于渠道的配置，并且设计为具有高可扩展性，支持多达10,000个类别树和每个类别树500个类别。 有关详细信息，请参阅[Merchandising Services开发人员指南](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/#categories)._中的_&#x200B;类别<!--DCAT-2649-->

### 其他发行说明

[!DNL Adobe Commerce Optimizer]使用最新版本的AEM Assets集成、Commerce Optimizer连接器和[!DNL Adobe Commerce Storefront]。 请使用以下链接查看每个区域的发行说明：

| 可扩展性 | 店面 |
| --- | --- |
| [AEM Assets集成](../aem-assets-integration/release-notes.md)<br>[Commerce Optimizer连接器](../aco-connector/release-notes.md) | [店面版本信息](https://experienceleague.adobe.com/developer/commerce/storefront/releases/)<br>[店面变更日志](https://experienceleague.adobe.com/developer/commerce/storefront/releases/changelog/) |

>[!ENDSHADEBOX]

## 2025年8月

**发行日期**：2025年8月28日

>[!BEGINSHADEBOX]

### 欧盟地区现已推出

欧盟地区(eu1)对客户IMS组织的支持现已可用。 在Cloud Manager中&#x200B;**添加Commerce Optimizer实例**&#x200B;时，您现在可以选择&#x200B;**欧盟**&#x200B;作为[地区](./get-started.md#step-1-create-an-instance)。 欧盟区域仅适用于生产环境。

欧盟区域的基本生产URL包括：

* 管理员： `https://eu1.admin.commerce.adobe.com`
* REST和GraphQL： `https://eu1.api.commerce.adobe.com`

![创建实例](./assets/create-instance.png){width="600" align="center" zoomable="yes"}

### 其他发行说明

[!DNL Adobe Commerce Optimizer]使用最新版本的AEM Assets集成、Commerce Optimizer连接器和[!DNL Adobe Commerce Storefront]。 请使用以下链接查看每个区域的发行说明：

| 可扩展性 | 店面 |
| --- | --- |
| [AEM Assets集成](../aem-assets-integration/release-notes.md)<br>[Commerce Optimizer连接器](../aco-connector/release-notes.md) | [店面版本信息](https://experienceleague.adobe.com/developer/commerce/storefront/releases/)<br>[店面变更日志](https://experienceleague.adobe.com/developer/commerce/storefront/releases/changelog/) |

>[!ENDSHADEBOX]
