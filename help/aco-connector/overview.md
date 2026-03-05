---
title: Adobe Commerce Optimizer连接器
description: 了解如何将Commerce云或内部部署项目中的数据连接到Adobe Commerce Optimizer
feature: Personalization, Integration, Configuration
badgePaas: label="仅限PaaS" type="Informative" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于云项目(Adobe管理的PaaS基础架构)和内部部署项目上的Adobe Commerce 。"
source-git-commit: 11bb5df2488a017065db44504f35612fe54e284c
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---


# Adobe Commerce Optimizer连接器

Adobe Commerce Optimizer Connector是一个集成桥，用于在云基础架构或内部部署上的Adobe Commerce与[!DNL Adobe Commerce Optimizer]之间同步目录和定价数据。 将数据同步到Adobe Commerce Optimizer可支持动态AI 搜索、推荐、网站优化和快速加载Headless存储前端等功能，包括Edge Delivery Services上的Adobe Commerce存储前端和实时性能分析。

## 架构和体验

Adobe Commerce Optimizer Connector的操作方式是将Commerce网站和存储区视图映射到Commerce Optimizer项目，如下图所示：

![将Commerce数据映射到Adobe Commerce Optimizer](./assets/storeview-to-catalogview-mapping.png){width="700" zoomable="yes"}

将数据从Commerce导出到Commerce Optimizer时：

* Commerce存储视图已映射到目录源
* 网站映射到价格手册

关联的目录和价格数据将导出，以后可用于创建目录视图，还可以选择定义策略以筛选特定业务用例的目录和价格数据。

启用连接器后，您还可以使用[[!DNL Adobe Commerce Optimizer] 促销工具](../optimizer/overview.md#quick-tour)配置和管理产品发现的促销规则和推荐规则。Adobe Commerce实例将成为目录和价格数据的数据源。 在Commerce中更新数据时，更新将同步到[!DNL Adobe Commerce Optimizer]实例。

## 工作流

连接器支持多个关键工作流：

* **将Commerce目录数据导出到[!DNL Adobe Commerce Optimizer]** — 在网站和客户组级别导出价格和价格手册数据。 产品和产品属性数据在`store view`级别导出。 默认情况下，所有Commerce作用域（网站和商店视图）的目录数据同步处于启用状态。

  要启用此工作流，请安装`adobe-commerce/commerce-data-export-aco-adapter` PHP扩展，检查导出器配置，然后从Commerce管理员中启用Commerce与Commerce Optimizer之间的集成。 有关详细说明，请参阅[开始使用](#get-started)。

* **映射Commerce网站和存储视图数据以导出到[!DNL Adobe Commerce Optimizer]**

  （可选）自定义导出设置以仅同步特定网站或商店视图的数据。 例如，您可以选择仅导出一个商店视图的目录数据以用于特定用例，如优化特定市场或区域的搜索和发现体验。

* **促销规则配置和管理**

  启用连接器后，将从[!DNL Adobe Commerce Optimizer] UI而不是从Commerce管理员的[!UICONTROL Live Search]和[!UICONTROL Product Recommendations]页面定义和管理产品发现和推荐的促销规则。

* **在Edge Delivery Services上部署您的Commerce店面**

  设置与[!DNL Adobe Commerce Optimizer]的集成后，您可以在Edge Delivery Services上部署Commerce店面。 这使用可组合、API驱动的体系结构提供了超快的性能、可扩展性、无缝的内容创作和集成的个性化。

有关如何设置集成和启用这些工作流的详细信息，请参阅[开始使用](get-started.md)。
