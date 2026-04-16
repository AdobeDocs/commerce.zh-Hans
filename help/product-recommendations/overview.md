---
title: ' [!DNL Product Recommendations]简介'
description: '[!DNL Product Recommendations]是一个强大的营销工具，可用于提高转化率、增加收入和刺激购物者参与。'
recommendations: noCatalog
badgePaas: label="仅限PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于云项目（Adobe管理的PaaS基础架构）和内部部署项目上的Adobe Commerce 。"
exl-id: 72850cfd-555c-4e0e-ac3e-097e6dac2030
source-git-commit: 1ae6b0f6786375ca4e7bb7620e164008a08f8965
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 0%

---

# [!DNL Product Recommendations]简介

产品推荐是一个强大的营销工具，可用于提高转化率、增加收入和刺激购物者参与。 Adobe Commerce产品推荐由[Adobe AI](https://business.adobe.com/ai.html)提供支持，它使用人工智能和机器学习算法来对汇总的访客数据进行深入分析。 此数据与Adobe Commerce目录结合使用后，可提供极具吸引力、相关且个性化的体验。

>[!IMPORTANT]
>
>**产品推荐不是HIPAA就绪的服务。**&#x200B;请勿在使用HIPAA就绪的产品或以其他方式处理受保护的健康信息(PHI)的任何Adobe Commerce实施中启用或使用产品推荐。 “产品推荐”是当前分类为不符合HIPAA要求的Commerce SaaS服务的一部分。
>
>有关哪些Adobe Commerce功能支持HIPAA以及哪些服务不能与PHI一起使用的详细信息，请参阅Adobe Commerce上的[HIPAA准备工作](https://experienceleague.adobe.com/en/docs/commerce-admin/start/compliance/hipaa-ready-service/overview)和[操作](https://experienceleague.adobe.com/en/docs/commerce-admin/start/compliance/hipaa-ready-service/operations#adobe-commerce-services)。

产品推荐以带标签的单位形式出现在店面上，例如“查看了这个产品的客户也查看了”。 您可以直接从Adobe Commerce管理员跨商店视图创建、管理和部署推荐。

如果店面是使用PWA Studio实现的，请参阅[PWA文档](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/)。 如果您使用自定义前端技术，如React或Vue JS，则了解如何[将](headless.md) [!DNL Product Recommendations]集成到Headless店面。

>[!NOTE]
>
>开发Headless或自定义实施的方法很多。 本指南将介绍使用PWA Studio实现此目标的一种方法。 它并未涵盖所有情景或事件。

## 隐私

为[!DNL Product Recommendations]目的的数据收集不包括任何个人身份信息(PII)。 此外，所有用户标识符（如Cookie ID和IP地址）都经过严格匿名处理。 若要了解更多信息，请参阅[Adobe隐私政策](https://www.adobe.com/privacy/policy.html)。

[!DNL Product Recommendations]用户可以参考[数据管理功能板](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html)，了解有关数据同步的更多数据。

## 产品推荐与产品关系

鉴于在线购物不断变化的复杂性，最适合您店面的往往是多种关键技术的组合。 同时使用[!DNL Product Recommendations]和[产品关系](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/product-relationships/product-relationships.html)可让您在促销产品时拥有更大的灵活性。 您可以利用由Adobe AI提供支持的[!DNL Product Recommendations]，大规模智能地自动执行您的推荐。 然后，在必须手动干预并确保向目标购物者区段提供特定推荐时，或者在必须满足某些业务目标时，您可以利用[相关产品规则](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/product-relationships/product-related-rules.html)。

通过产品推荐，您可以：

- 根据以下领域从九种不同的智能推荐类型中进行选择：基于购物者、基于项目、基于人气、趋势和基于相似度
- 使用行为数据在整个购物者的店面历程中个性化推荐
- 衡量与每个推荐相关的关键量度，以帮助您了解推荐的影响

## [!DNL Product Recommendations]演示

观看此视频以了解[!DNL Product Recommendations]：

>[!VIDEO](https://video.tv.adobe.com/v/343991?quality=12)

## 目录数据保留策略

如果您连续90天没有在测试环境中提交对目录数据的查询，则目录数据将设置为休眠模式，并且任何查询都不会返回任何数据。 此策略不会影响生产环境中的目录数据。

### 不活动的测试环境

要在测试环境中重新激活目录数据，请[提交标题为“重新激活](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#experience-league-start-page)”的支持请求[!DNL Product Recommendations]并包含环境ID。 测试环境中的目录数据应在几小时内恢复。

### 清空目录

如果您的环境在创建后45天内有一个空目录，则目录数据将设置为休眠模式，并且任何查询都不会返回任何数据。 这包括生产和测试环境。

要在您的环境中重新激活目录数据，请[提交标题为“重新激活](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#experience-league-start-page)”的支持请求[!DNL Product Recommendations]并包含环境ID。 您环境中的目录数据应会在几小时内恢复。
