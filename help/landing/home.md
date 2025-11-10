---
title: 服务指南主页
description: 浏览Commerce SaaS服务的Adobe Commerce产品文档
seo-title: Services for Adobe Commerce
seo-description: Access the product documentation for hosted services that help Adobe Commerce merchants support key components of their business.
recommendations: noCatalog
exl-id: 507af1fa-9f3e-41bc-9aaf-cd89839aae0b
source-git-commit: fd3857e93dbaaf7ffce97715b77ee63e8460af16
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 0%

---

# Adobe Commerce Services指南

Adobe Commerce服务提供强大的功能，可扩展您的店面、简化集成和优化数据管理。

## Commerce如何连接到服务？

所有Commerce服务都通过[Commerce服务连接器](saas.md)连接到您的Commerce实例。

配置Commerce服务连接器后，您可以访问以下功能：

- [店面服务](#storefront-services) — 用于产品发现、推荐和付款的AI支持功能
- [集成服务](#integration-services) — 连接到Adobe Experience Platform、AEM Assets和其他Adobe解决方案

这些服务可帮助您提高转化率，提供个性化体验，并更好地利用整个Adobe生态系统的商业数据。

![服务层](./assets/services-layer.png)

>[!NOTE]
>
>Adobe建议升级到所有Commerce服务的最新支持版本。 请参阅[发行说明](release-notes-all.md)。

除了这些功能之外，还有一些工具可让您监控从Commerce实例到SaaS平台的数据流。 这些工具可以自动同步数据，并帮助您优化性能。 了解有关可用[数据工具](#data-tools)的详细信息。

## 可用服务

>[!BEGINTABS]

>[!TAB 店面服务]

Storefront服务是一组AI支持的功能，可优化产品发现、个性化客户交互和简化支付处理以提高参与度和转化率。 借助店面服务，您可以改善购物体验并推动业务增长。

<table style="table-layout:fixed">
<tr style="border: 0;">
   <td valign="top">
      <a href="../catalog-service/overview.md">
      <img alt="连接的服务的目录数据" src="../assets/icons/DataBook.svg" width="40">
      </a>
      <div>
         <a href="../catalog-service/overview.md">
         <strong>目录服务</strong>
         </a>
      </div>
      <p>
         <em>为您的客户提供优化的产品体验，同时提高性能、改进可扩展性和提高转化率。</em>
      </p>
   </td>
   <td valign="top">
      <a href="../live-search/overview.md">
      <img alt="Search" src="../assets/icons/Magnify.svg" width="40">
      </a>
      <div>
         <a href="../live-search/overview.md">
         <strong>[!DNL Live Search]</strong>
         </a>
      </div>
      <p>
         <em>实施此AI支持的搜索工具，为B2C购物者提供更智能、更快和更相关的结果。</em>
      </p>
   </td>
   <td valign="top">
      <a href="../product-recommendations/overview.md">
      <img alt="竖起大拇指" src="../assets/icons/ThumbUp.svg" width="40">
      </a>
      <div>
         <a href="../product-recommendations/overview.md">
         <strong>产品推荐</strong>
         </a>
      </div>
      <p>
         <em>根据购物者行为、流行趋势、产品相似性等添加AI支持的推荐。</em>
      </p>
   </td>
   <td valign="top">
      <a href="../payment-services/guide-overview.md">
      <img alt="信用卡付款" src="../assets/icons/CreditCard.svg" width="40">
      </a>
      <div>
         <a href="../payment-services/guide-overview.md">
         <strong>付款服务</strong>
         </a>
      </div>
      <p>
         <em>通过多种付款方式提高客户满意度，包括免息分期付款，以及简化付款处理、订单和发票的查看。</em>
      </p>
   </td>
</tr>
</table>

>[!TAB 集成服务]

集成服务是指将您的Commerce实例连接到Adobe中其他产品或服务的功能。

<table style="table-layout:fixed">
<tr style="border: 0;">
   <td valign="top">
      <a href="../data-connection/overview.md">
      <img alt="将数据传输到平台" src="../assets/icons/TransferToPlatform.svg" width="40">
      </a>
      <div>
         <a href="../data-connection/overview.md">
         <strong>[!DNL Data Connection]</strong>
         </a>
      </div>
      <p>
         <em>利用Adobe Commerce和Adobe Experience Platform Edge之间的连接将Commerce数据用于其他Adobe Experience Cloud产品，如Adobe Analytics和Adobe Target。</em>
      </p>
   </td>
   <td valign="top">
      <a href="../aem-assets-integration/overview.md">
      <img alt="可视化" src="../assets/icons/images.svg" width="40">
      </a>
      <div>
          <a href="../aem-assets-integration/overview.md">
         <strong>AEM Assets集成</strong>
         </a>
      </div>
      <p>
         <em>使用与Adobe Experience Manager集成的系统简化数字资源管理，以便管理富媒体内容。</em>
      </p>
   </td>
</tr>
</table>

>[!TAB 数据工具]

数据工具可帮助您管理和优化Commerce实例与所连接服务之间的信息流。 这些工具可确保高效的数据同步、监控同步操作，并通过卸载资源密集型进程来提高性能。

<table style="table-layout:fixed">
<tr style="border: 0;">
   <td valign="top">
       <a href="../data-export/overview.md">
      <img alt="SaaS数据导出信息源管理" src="../assets/icons/FeedManagement.svg" width="40">
      </a>
      <div>
         <a href="../data-export/overview.md">
         <strong>[!DNL SaaS Data Export]</strong>
         </a>
      </div>
      <p>
         <em>自动将目录、订单和清单数据从Adobe Commerce同步到连接的服务。 使用Commerce CLI命令或<strong>数据管理功能板</strong>管理同步处理。</em>
      </p>
   </td>
   <td valign="top">
      <a href="../price-index/price-indexing.md">
      <img alt="产品价格信息源" src="../assets/icons/Feed.svg" width="40">
      </a>
      <div>
          <a href="../price-index/price-indexing.md">
         <strong>SaaS价格索引器</strong>
         </a>
      </div>
      <p>
         <em>通过从Commerce应用程序向Adobe的云基础架构转移大量占用资源的任务（如索引和价格计算），优化站点性能。</em>
      </p>
   </td>
   <td valign="top">
      <a href="https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard" target="_blank">
      <img alt="监控数据同步" src="../assets/icons/Monitoring.svg" width="40">
      </a>
      <div>
          <a href="https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard" target="_blank">
         <strong>数据管理仪表板</strong>
         </a>
      </div>
      <p>
         <em>在Commerce管理员中，轻松地跟踪统一仪表板的Commerce数据同步并触发重新同步。 获取有关数据可用性的宝贵见解，以便及时向购物者显示。</em>
      </p>
   </td>
</table>

>[!NOTE]
>
>使用Product Recommendations v6.0.0、Live Search v4.1.0或目录服务v1.17并具有有效许可证的Commerce商家可以免费使用数据管理功能板。 使用早期服务版本的商家可以使用[目录同步](../landing/catalog-sync.md)来管理和跟踪数据同步。

>[!ENDTABS]

## Commerce服务可以解决哪些问题？

无论您是希望扩展业务、改善客户体验还是做出数据驱动型决策，Adobe Commerce服务都能提供解决方案来解决常见的Commerce挑战：

| 问题 | 挑战 | 解决方案 |
|---------|-----------|----------|
| 改进产品发现和转换 | 购物者找不到他们想要的东西，导致跳出率很高，销售额也出现下滑。 | 使用[实时搜索](../live-search/overview.md)和[产品推荐](../product-recommendations/overview.md)，基于实时购物者行为提供具有拼写容错、即时“键入时搜索”结果、动态彩块化和个性化产品推荐的AI支持搜索。 |
| 创建全渠道个性化体验 | 您的商业数据处于孤立状态，使您无法跨渠道提供个性化体验。 | 使用[Data Connection](../data-connection/overview.md)将行为、事务性和用户档案数据发送到Adobe Experience Platform。 构建复杂的客户区段，创建放弃的购物车促销活动，定位相似受众，并分析整个客户历程中的季节性趋势。 |
| 简化数字资产管理 | 跨多个系统管理产品映像和富媒体非常耗时且容易出错。 | [AEM Assets集成](../aem-assets-integration/overview.md)通过将Adobe Commerce连接到Adobe Experience Manager Assets项目、简化工作流并确保在所有接触点上提供一致的品牌体验，提供了集中式资产管理。 |
| 优化支付处理 | 支付选项有限和支付体验缺佳损害了客户满意度和转化率。 | [付款服务](../payment-services/guide-overview.md)提供多种付款方式，包括免息分期付款，并有一个统一的信息板来管理付款、订单和发票。 |
| 大规模管理数据同步 | 资源密集型索引正在减慢网站速度，并且您无法轻松跟踪数据同步问题。 | [SaaS数据导出](../data-export/overview.md)、[SaaS价格索引器](../price-index/price-indexing.md)和[数据管理仪表板](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)自动同步目录、订单和库存数据，将价格计算卸载到Adobe的云基础架构，并实时查看同步状态。 |
| 挽回失去的客户并减少回报 | 高客户流失率和产品回报率正在影响盈利能力。 | 将[Data Connection](../data-connection/overview.md)与Adobe Journey Optimizer和Real-Time CDP结合使用，以识别返回模式、创建回馈促销活动、按行为划分客户区段，以及通过电子邮件和短信发送个性化的重新参与促销活动。 |
| 制定数据驱动型促销决策 | 您不确定要促销哪些产品或者何时运行促销活动。 | [实时搜索](../live-search/overview.md)提供搜索性能洞察和促销工具，用于访问关键量度、分析搜索词以及使用智能促销规则来根据真实的客户行为和业务目标提升或隐藏产品。 |
| 维护对敏感数据的合规性 | 您需要处理敏感的客户数据，同时保持HIPAA合规性。 | [Data Connection](../data-connection/overview.md)支持HIPAA，允许您与Experience Platform共享后台数据，同时保持合规性并系统地处理隐私请求。 |

{{$include /help/_includes/templated/whats-new.md}}

<!-- Last updated from includes: 2025-09-26 20:42:12 -->
