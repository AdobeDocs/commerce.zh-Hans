---
title: 什么是产品推荐？
description: 了解Adobe Commerce中的产品推荐。 探索人工智能驱动的店面单元、隐私、管理和店面路径以及关键数据保留。
recommendations: noCatalog
exl-id: 72850cfd-555c-4e0e-ac3e-097e6dac2030
source-git-commit: 6bfc2c0ed53b44fb30a142dc87f87dca8a601a33
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 0%

---

# 什么是[!DNL Product Recommendations]？

[!DNL Product Recommendations]可帮助您使用[Adobe AI](https://business.adobe.com/cn/ai.html)在Adobe Commerce店面上显示个性化产品推荐，并使用机器学习了解汇总购物者行为和您的目录。 此概述涵盖了服务限制（包括HIPAA）、数据和隐私（推荐单元出现的位置）、店面实施路径、推荐如何补充产品关系以及目录数据保留。

>[!IMPORTANT]
>
>**[!DNL Product Recommendations]不是HIPAA就绪的服务。** 请勿在使用HIPAA就绪产品或以其他方式处理受保护的健康信息(PHI)的任何Adobe Commerce实现中启用或使用[!DNL Product Recommendations]。 [!DNL Product Recommendations]属于当前分类为不符合HIPAA要求的Commerce SaaS服务。
>
>有关哪些Adobe Commerce功能支持HIPAA以及哪些服务不能与PHI一起使用的详细信息，请参阅Adobe Commerce上的[HIPAA准备工作](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/start/compliance/hipaa-ready-service/overview)和[操作](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/start/compliance/hipaa-ready-service/operations#adobe-commerce-services)。

## 数据处理和隐私

[!DNL Product Recommendations]的数据收集不包括任何个人身份信息(PII)。 所有用户标识符（如Cookie ID和IP地址）都经过严格匿名处理。 若要了解更多信息，请参阅[Adobe隐私政策](https://www.adobe.com/privacy/policy.html)。

有关数据同步的详细信息，请参阅[数据管理功能板](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html?lang=zh-Hans)。

## 显示推荐的位置

推荐作为带有标签的单位显示在店面上，例如“查看过此产品的客户也查看过”。 您可以通过Adobe Commerce管理员，跨商店视图创建、管理和部署推荐。 如果您的Commerce项目使用[Adobe Commerce Optimizer Connector](https://experienceleague.adobe.com/zh-hans/docs/commerce/aco-optimizer-connector/overview)，则可以通过[Adobe Commerce Optimizer](../optimizer/overview.md)创建、管理和部署推荐。

## 店面实施

选择与您的店面匹配的文档：

- **PWA Studio** — [PWA文档](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/)
- **自定义店面（例如，React或Vue.js）** — [在Headless店面中集成 [!DNL Product Recommendations]](headless.md)
- **Commerce Edge Delivery Services (EDS)** — [EDS的Adobe Commerce Storefront文档](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/?lang=zh-Hans)

>[!NOTE]
>
>Headless和自定义设置因栈栈而异。 本产品区域记录了PWA Studio路径和常规Headless集成模式；它并未涵盖每个第三方或自定义场景。

## 产品推荐与产品关系

鉴于在线购物不断变化的复杂性，最适合您店面的往往是多种关键技术的组合。 同时使用[!DNL Product Recommendations]和[产品关系](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/product-relationships/product-relationships.html?lang=zh-Hans)可让您在促销产品时拥有更大的灵活性。 您可以利用由Adobe AI提供支持的[!DNL Product Recommendations]，大规模智能地自动执行您的推荐。 然后，在必须手动干预并确保向目标购物者区段提供特定推荐时，或者在必须满足某些业务目标时，您可以利用[相关产品规则](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/product-relationships/product-related-rules.html?lang=zh-Hans)。

通过产品推荐，您可以：

- 根据以下领域从九种不同的智能推荐类型中进行选择：基于购物者、基于项目、基于人气、趋势和基于相似度
- 使用行为数据在整个购物者的店面历程中个性化推荐
- 衡量与每个推荐相关的关键量度，以帮助您了解推荐的影响

## 产品推荐演示

观看此视频以了解[!DNL Product Recommendations]：

>[!VIDEO](https://video.tv.adobe.com/v/343991?quality=12)

## 目录数据保留策略

[!DNL Product Recommendations]服务依赖于与您的Adobe Commerce环境保持同步的目录数据。 停止查询数据的非活动目录或环境可以进入休眠，这会影响在您重新激活之前服务返回的内容。

如果您连续90天未在&#x200B;**测试**&#x200B;环境中提交对目录数据的查询，则目录数据将设置为休眠模式，并且任何查询都不会返回任何数据。 **生产**&#x200B;环境中的目录数据不受90天规则的影响。

如果您的环境在创建45天后有&#x200B;**空目录**，则目录数据将设置为休眠模式，并且不会为任何查询返回任何数据。 这同时适用于生产和测试环境。

### 重新激活目录数据

要在休眠后还原目录数据，请[提交标题为“重新激活[!DNL Product Recommendations]”的支持请求](https://experienceleague.adobe.com/zh-hans/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#experience-league-start-page)并包含环境ID。 目录数据应会在几小时内恢复。
