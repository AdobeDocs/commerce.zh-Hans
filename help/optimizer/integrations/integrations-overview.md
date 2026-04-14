---
title: Commerce Optimizer集成
description: 了解针对目录同步、资源管理、店面优化和Salesforce Commerce Cloud连接的Adobe Commerce Optimizer集成。
solution: Commerce
feature: Integration, Catalog Management
role: Developer, Admin
level: Beginner
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于 [!DNL Adobe Commerce Optimizer] 个项目（Adobe管理的SaaS基础结构）。"
exl-id: 8f3a2c1b-9d4e-5f6a-bc7d-1e2f3a4b5c6d
source-git-commit: d8cd6f543353e1b11f3aa14b3b97b02155d23809
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---


# [!DNL Adobe Commerce Optimizer]集成

[!DNL Adobe Commerce Optimizer]包括的集成允许您在云上或内部部署中从Adobe Commerce同步数据、管理资源、改进店面体验以及连接外部系统。 以下各节将介绍每个集成如何与[!DNL Adobe Commerce Optimizer]配合使用。 按照这些链接进行设置、配置和日常使用。

## Adobe Commerce Optimizer连接器 {#aco-connector}

Adobe Commerce Optimizer Connector是在Adobe Commerce（云或内部部署）和[!DNL Adobe Commerce Optimizer]之间同步目录和定价数据的桥梁。 启用连接器后，Commerce将保留产品数据的记录系统，而[!DNL Adobe Commerce Optimizer]将支持产品发现、推荐、促销规则、分析和Headless店面体验。

- [Adobe Commerce Optimizer连接器概述](../../aco-connector/overview.md){target="_blank"}
- [开始使用连接器](../../aco-connector/get-started.md){target="_blank"}

## AEM Assets的产品可视化图表 {#product-visuals}

产品可视化图表允许您通过Adobe Experience Manager (AEM) Assets管理产品图像。 配置适用于Commerce Optimizer的AEM Assets以启用产品可视化图表。 完成配置后，您可以将AEM Assets用作产品映像的集中数字资产管理解决方案，它提供了自动资源审查和管理工作流，使映像与Commerce Optimizer目录保持同步。 该集成按SKU匹配资产和产品。 更新通过Adobe的集成服务流动，因此店面无需手动重新上传即可反映最新媒体。

- [AEM Assets的产品可视化图表](../setup/product-visuals.md)
- [为Commerce Optimizer配置AEM Assets](../../aem-assets-integration/get-started/configure-aco.md){target="_blank"}

## Adobe Experience Manager Sites Optimizer {#aem-sites-optimizer}

Adobe Experience Manager Sites Optimizer分析Commerce网站并通过显示AI驱动的&#x200B;**[!UICONTROL Opportunities]**&#x200B;来提高性能 — 这些建议可帮助您提高发现、参与和转化率。

>[!AVAILABILITY]
>
>此功能需要&#x200B;**Ultima** Adobe Sites Optimizer许可证。 您可以通过Adobe客户技术顾问申请许可证。 配置帐户后，[!DNL Adobe Commerce Optimizer]界面中将提供“机会”功能，您可以开始使用AI驱动的见解来优化店面和促销策略。

- [机会](../manage-results/opportunities.md)

## Commerce Salesforce Connector {#commerce-salesforce-connector}

Commerce Salesforce Connector（基于Adobe App Builder构建）将Salesforce Commerce Cloud B2C中的目录和价格数据同步到[!DNL Adobe Commerce Optimizer]中，以便您可以使用Adobe店面和促销功能，而无需重新部署Salesforce Commerce后端。 您可以使用Salesforce Commerce API计划同步、运行按需更新并扩展集成。

- [Salesforce Commerce Connector](../developer/salesforce-connector.md)

>[!MORELIKETHIS]
>
>- [Adobe Commerce Optimizer技术文档](https://developer.adobe.com/commerce/services/optimizer/){target="_blank"}
>- [开始使用Adobe Commerce Optimizer](../get-started.md)
