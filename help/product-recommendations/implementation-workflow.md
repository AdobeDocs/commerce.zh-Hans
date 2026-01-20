---
title: 实施工作流
description: 了解在您的店面成功实施 [!DNL Product Recommendations] 的步骤。
exl-id: 4a784d04-8be6-473f-afb3-264af06c850a
source-git-commit: 458f34c45406db871ec61ff408aa624f163b6ee0
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# 实施工作流

[!DNL Product Recommendations]同时使用行为和目录数据：

- 行为 — 购物者在您网站上的参与数据，例如产品查看次数、添加到购物车的商品数，以及购买次数。 Adobe Commerce和Adobe AI不会收集个人身份信息。

- 目录 — 产品元数据，如名称、价格和可用性。

安装`magento/product-recommendations module`时，Adobe AI会聚合行为和目录数据并为每个推荐类型创建[!DNL Product Recommendations]。 然后，[!DNL Product Recommendations]服务将这些推荐部署到您的店面。 要帮助您在店面中实施产品推荐，请使用以下工作流：

>[!NOTE]
>
> 如果店面是使用PWA Studio实现的，请参阅[PWA文档](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/)。 如果您使用自定义前端技术，如React或Vue JS，则了解如何[将](headless.md) [!DNL Product Recommendations]集成到Headless店面。

## 工作流

1. **将数据集合部署到生产环境**

   部署[!DNL Product Recommendations]需要两个主要[数据源](type.md)：目录和行为。 由于生产是捕获和分析购物者行为的唯一环境，因此请尽早在生产上开始收集数据。 [了解](events.md)Adobe AI如何训练可产生更高质量推荐的机器学习模型。 作为一项附加好处，当您开始收集生产上的行为数据时，可以在非生产环境中操作时基于此生产数据[获取推荐](staging-environment.md#fetch-recommendations-from-production-environment-recommended)。 然后，您可以测试和试验根据在生产过程中收集的实际购物者数据计算的各种推荐。

   要将数据收集部署到生产环境，您必须[通过提供](install-configure.md)API密钥[!DNL Product Recommendations]来安装和配置[ ](https://experienceleague.adobe.com/docs/commerce/user-guides/integration-services/saas.html)模块。

   >[!TIP]
   >
   > 部署数据收集不会更改店面的外观或购物者的体验。 只有创建和部署推荐单元才能改变店面的客户体验。 在部署到生产环境之前，请确保在非生产环境中进行测试。 此外，在自定义模板之前，请勿创建推荐单位。 请参阅下一步。

1. **自定义模板以匹配您的样式**

   您的店面代表您的品牌，因此请确保修改产品推荐模板以匹配您的站点主题。

   >[!TIP]
   >
   > 通过自定义模板，您可以指定样式表、覆盖推荐单元在页面上出现的位置等等。

   请参阅开发人员文档中的[自定义](https://experienceleague.adobe.com/docs/commerce/product-recommendations/developer/customize.html)，了解如何完成此步骤。

1. **在非生产环境中测试推荐**

   在部署到生产环境之前，最好在非生产环境中测试一项新技术。 通过在非生产环境中测试推荐，您可以播放不同的推荐单元类型、位置和页面。 您可以在非生产环境中执行测试时，根据已在生产环境中收集的行为数据提取推荐，这样推荐结果就会基于实际客户的购物行为。

   >[!TIP]
   >
   > 确保您的非生产环境目录与生产环境中的目录大致相同。 使用类似的目录可确保推荐单元中返回的产品与生产中的产品非常相似。

   请参阅从生产环境获取[行为数据](staging-environment.md)以了解如何完成此步骤。

1. **创建推荐并将其部署到您的生产店面**

   现在，您已在生产环境中部署行为数据收集，修改了产品推荐模板，并且使用实际的购物者行为对推荐进行了测试，接下来可以将所有代码提升到生产环境中并[创建](create.md)实时产品推荐。
