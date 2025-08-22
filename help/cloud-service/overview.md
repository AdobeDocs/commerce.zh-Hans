---
title: '[!DNL Adobe Commerce as a Cloud Service] 概述'
description: 了解 [!DNL Adobe Commerce as a Cloud Service]的主要功能和优势。
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Architect, Developer, User, Leader
exl-id: 1b7e2731-4a10-4c2b-9bfc-8945729ed523
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目(Adobe管理的SaaS基础架构)。"
source-git-commit: 8fc46b0b93ac5102477f33bf2a8ae70a7acaf85d
workflow-type: tm+mt
source-wordcount: '1405'
ht-degree: 0%

---


# [!DNL Adobe Commerce as a Cloud Service] 概述

[!DNL Adobe Commerce as a Cloud Service]通过使企业能够交付并快速扩展数字运营并加快创新，提供了灵活性、可扩展性和效率。 Adobe的云原生基础架构可自动调整资源，以满足流量、订单和目录管理的峰值需求。

下表突出显示支持[!DNL Adobe Commerce as a Cloud Service]的产品：

<table style="table-layout:auto">
  <tr>
    <td>
      <span style="display: inline-block; width: 20px; height: 20px; background: white; border: 1px solid #d32f2f; border-radius: 50%; margin-right: 8px; vertical-align: middle;">
        <span style="color: #d32f2f; font-size: 14px; line-height: 18px; display: block; text-align: center;">✓</span>
      </span>
      <strong>Commerce店面</strong>
    </td>
    <td>
      面向客户的界面，购物者可在此浏览和购买产品
    </td>
  </tr>
  <tr>
    <td>
      <span style="display: inline-block; width: 20px; height: 20px; background: white; border: 1px solid #d32f2f; border-radius: 50%; margin-right: 8px; vertical-align: middle;">
        <span style="color: #d32f2f; font-size: 14px; line-height: 18px; display: block; text-align: center;">✓</span>
      </span>
      <strong>促销服务</strong>
    </td>
    <td>
      管理产品目录、定价和库存的后端服务
    </td>
  </tr>
  <tr>
    <td>
      <span style="display: inline-block; width: 20px; height: 20px; background: white; border: 1px solid #d32f2f; border-radius: 50%; margin-right: 8px; vertical-align: middle;">
        <span style="color: #d32f2f; font-size: 14px; line-height: 18px; display: block; text-align: center;">✓</span>
      </span>
      <strong>产品视觉效果</strong>
    </td>
    <td>
      产品图像和媒体的数字资产管理
    </td>
  </tr>
  <tr>
    <td>
      <span style="display: inline-block; width: 20px; height: 20px; background: white; border: 1px solid #d32f2f; border-radius: 50%; margin-right: 8px; vertical-align: middle;">
        <span style="color: #d32f2f; font-size: 14px; line-height: 18px; display: block; text-align: center;">✓</span>
      </span>
      <strong>开发人员平台</strong>
    </td>
    <td>
      用于构建自定义功能的核心开发工具和API
    </td>
  </tr>
</table>

## 架构

请观看以下视频，了解[!DNL Adobe Commerce as a Cloud Service]架构的简介。 视频下方提供了说明体系结构的图。

>[!VIDEO](https://video.tv.adobe.com/v/3443277?learn=on&captions=chi_hans)

此图说明了[!DNL Adobe Commerce as a Cloud Service]和所有Adobe Experience Cloud解决方案之间的数据流。

![[!DNL Adobe Commerce as a Cloud Service]架构图](./assets/data-flow.svg){zoomable="yes"}

## Commerce店面

使用由Edge Delivery Services提供支持的Adobe [Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront?lang=zh-Hans)，通过Storefront Builder的基于文档的简单创作或可视化编辑，在几分钟内创建丰富的体验。

Commerce Storefront是完全无头的，具有解耦的架构，通过GraphQL API层提供所有促销服务和数据。 此架构允许团队独立于Commerce Foundation开发其前台，从而提供使用新兴技术构建和测试新接触点的灵活性。

>[!NOTE]
>
>[!DNL Adobe Commerce as a Cloud Service]不支持Luma店面。 如果您是从Adobe Commerce在云中或内部部署迁移，请参阅[现有店面](https://experienceleague.adobe.com/developer/commerce/storefront/discovery/?lang=zh-Hans#existing-storefronts)以获取有关过渡的指导。

## 商品推销服务和支付服务

Adobe提供了一组丰富的智能、可组合的推销服务，帮助您支持关键业务目标。 这些服务还提供了对大规模优化性能至关重要的API。

- [实时搜索](../live-search/overview.md) — 通过此AI支持的搜索工具，为购物者提供更智能、更快速且相关的结果。
- [产品推荐](../product-recommendations/overview.md) — 根据购物者行为、流行趋势、产品相似性等添加AI驱动的推荐。
- [由目录视图和策略提供支持的促销服务](../optimizer/setup/catalog-view.md) — 通过灵活的数据建模管理大型且复杂的产品目录，以提供与业务结构和上市战略相一致的性能高、灵活的商务目录。 与[Commerce Optimizer](../optimizer/overview.md)一起使用可优化目录性能并提高转化率。
- [支付服务](../payment-services/guide-overview.md) — 通过提供各种支付方式（包括免息分期付款）和单一付款处理、订单和发票视图，提高客户满意度。

## 由AEM Assets提供支持的产品视觉效果

产品可视化图表使用数字资源管理(DAM)系统来帮助简化资源管理，该系统与Adobe Experience Manager集成以管理富媒体内容。

该集成可确保根据SKU或其他关键属性，将数字资产（如产品图像或营销内容）动态链接到相应的促销实体，包括Adobe Commerce中的产品和类别。

产品可视化图表现成可用于[!DNL Adobe Commerce as a Cloud Service]，提供了AEM Assets的一些功能。

或者，[!DNL Adobe Commerce as a Cloud Service]中的本机功能提供了用于存储和管理数字资产的基本资产管理工具。

### 产品可视化图表或AEM Assets

以下比较可帮助您选择最符合内容供应链需求的选项：

<table style="width: 100%; border-collapse: collapse; margin: 20px 0;">
  <tr style="border: none;">
    <td style="width: 45%; vertical-align: top; border: 2px solid #e0e0e0; padding: 20px; background: #fafafa;">
      <p style="color: #d32f2f; border-bottom: 2px solid #d32f2f; padding-bottom: 10px; margin-top: 0;">由AEM Assets提供支持的产品视觉效果</h3>
      <ul style="margin: 0; padding-left: 20px;">
        <li>集成的自动化产品图像和视频Digital Asset Manager (DAM)</li>
        <li>调整图像大小、裁切和转换图像</li>
        <li>高速图像和视频传送</li>
        <li>根据客户端浏览器功能优化图像格式、大小和质量</li>
        <li>访问Adobe Express和Adobe Firefly</li>
        <li>图像/视频投放容量和用户访问的使用限制</li>
        <li>集成的资产选择器</li>
      </ul>
    </td>
    <td style="width: 10%; text-align: center; vertical-align: middle; font-size: 98px; color: #d32f2f; font-weight: bold;">
      ’
    </td>
    <td style="width: 45%; vertical-align: top; border: 2px solid #e0e0e0; padding: 20px; background: #fafafa;">
      <p style="color: #d32f2f; border-bottom: 2px solid #d32f2f; padding-bottom: 10px; margin-top: 0;">AEM Assets</h3>
      <ul style="margin: 0; padding-left: 20px;">
        <li>产品可视化图表的所有功能</li>
        <li>Full marketing Digital Asset Manager (DAM)</li>
        <li>无限制用户（按用户付费）</li>
        <li>无限制的图像和视频交付</li>
        <li>高级资产管理功能：</li>
        <ul>
          <li>360°旋转集和交互式查看器</li>
          <li>3D模型支持和沉浸式内容</li>
          <li>PDF支持</li>
          <li>AI支持的智能裁剪</li>
         <li>动态图像模板</li>
        <li>智能标记</li>
        <li>跟踪和分析资产性能</li>
        </ul>
      </ul>
    </td>
  </tr>
</table>

<table style="width: 100%; margin: 20px 0;">
  <tr>
    <td style="background: #f5f5f5; padding: 15px; text-align: center; font-weight: bold;">
      Adobe品牌集成可用于轻松在产品之间迁移。
    </td>
  </tr>
</table>

请参阅[AEM Assets集成](../aem-assets-integration/overview.md)指南，详细了解如何将由AEM Assets支持的产品可视化与[!DNL Adobe Commerce as a Cloud Service]集成。

## 开发人员平台

Adobe为开发人员提供了全面的扩展点和工具，用于构建可扩展Commerce Foundation功能并与第三方系统（如CRM、ERPS和PIMS）集成的应用程序。 这些工具可通过以下方式降低平台的总拥有成本：

- **可扩展性** — 应用程序可以与核心软件分开扩展，以便提高效率和简化升级。
- **隔离** — 隔离环境意味着开发人员可以自行升级或修改其扩展，而无需依赖核心版本。
- **技术独立性** — 开发人员可以选择任何符合其需求的技术栈栈和编码语言。

>[!TIP]
>
>供应商构建的应用也可用于在[Adobe Exchange](https://exchange.adobe.com/)上安装。

Adobe提供了以下开发人员工具来构建集成和自定义：

- Adobe Developer App Builder的&#x200B;[**API网格**](https://developer.adobe.com/graphql-mesh-gateway/) — 协调多个API、GraphQL、REST和其他源并将其合并到一个可查询的GraphQL端点中。
- [**App Builder**](https://developer.adobe.com/app-builder/docs/overview/) — 构建并部署安全且可扩展的Web应用程序，这些应用程序可扩展Commerce功能并与第三方解决方案集成。
- [**事件**](https://developer.adobe.com/commerce/extensibility/events/) — 使用自定义事件触发器与其他可扩展开发工具交互。
- [**Webhooks**](https://developer.adobe.com/commerce/extensibility/webhooks/) — 使用Webhook自动触发Commerce与第三方系统之间的交互。
- [**管理员UI SDK**](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/) — 使用商户的新页面和功能自定义并增强Commerce管理员。
- [**集成入门工具包**](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/) — 通过参考集成、入门脚本和标准化架构加速您的后台集成。

## Commerce Foundation

Commerce Foundation提供了一个安全的自动托管平台和自助服务功能，用于在云原生环境中管理Commerce应用程序。

主要功能包括：

- 简化的入门
- 无缝升级
- 第三方集成

### 简化的入门

使用[!UICONTROL Commerce Cloud Manager]自助配置门户在几分钟内启动沙盒和生产实例。 您需要的所有功能(包括促销服务、Headless Commerce实例和App Builder)均可自动配置并与实例集成。

请参阅[快速入门](getting-started.md)，了解如何创建和管理Commerce实例。

### 无缝升级

无需手动升级即可访问最新的功能和增强功能。 持续提供新功能和更新消除了手动修补的需要，确保您始终能够以较低的总体拥有成本访问最新功能。

Adobe Commerce on Cloud的典型升级过程包括创建备份、克隆实例、运行兼容性工具以及修复代码冲突。 对于[!DNL Adobe Commerce as a Cloud Service]不再需要。 发布新功能和安全更新后，Adobe会向您发送应用程序内通知。 您有30天的时间评估沙盒实例中的新功能，之后更新将自动应用于生产环境。

>[!NOTE]
>
>Adobe保证所有更新的向后兼容性。 这意味着应用更新时，不会破坏符合[API优先可扩展性](https://developer.adobe.com/commerce/extensibility/)模型的现有功能或自定义设置。

### 第三方集成

开发人员可以使用全面的[GraphQL](https://developer.adobe.com/commerce/webapi/graphql/)和[REST API](https://developer.adobe.com/commerce/webapi/rest/)将Commerce Foundation与第三方系统集成并扩展Commerce功能。

<!-- ## Experience Cloud integration

[!DNL Adobe Commerce as a Cloud Service] integrates with all Experience Cloud solutions to deliver [personalized commerce experiences at scale](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/customers/customers-menu/personalize-scale#customers-menu).

[Data Connection](../data-connection/overview.md) unlocks insights about your shoppers' buying behavior so that you can create personalized shopping experiences across all channels with other Adobe Digital Experience products. -->

## 优点

以下部分提供了有关[!DNL Adobe Commerce as a Cloud Service]为业务和IT领导提供的好处的信息。

### 商业领袖

- **增加收入**：使用可提升SEO的高性能店面提高自然流量。 创建个性化体验，使用丰富数据推动转化。
- **扩展运营**：自动扩展服务以99.9%的可用性满足您业务的高峰需求。 转出多个品牌和区域，并从单个实例中支持B2B和B2C。 通过灵活的数据建模支持大型和复杂的产品目录。
- **提高推销员的工作效率**：使用AI支持的推销服务提高转化率。 直接在店面进行原生试验。 通过简单的基于文档的创作或可视编辑器管理店面体验，在几分钟内创建丰富的体验。
- **降低总拥有成本(TCO)并加快创新**：始终保持最新的服务让您能够立即访问新功能。 通过轻松地从市场安装应用程序来激活新功能。 将资源从繁琐的维护中释放出来，集中精力构建新功能。

### 信息技术(IT)领导者

- **快速配置**：在几分钟内快速开始自助配置。 所有服务都已预先配置为无缝协作，以便更快地启动。 根据需要为开发人员实验配置沙盒。
- **拥有成本低**：不再升级始终保持最新的服务。 使用自动为您应用的最新安全补丁程序，确保安全和合规性。 自动扩展以满足最苛刻的工作负载。
- **高性能店面**：使用简单的基于文档的创作或可视化编辑器，在几分钟内创建丰富的体验。 使用AI支持的促销服务来提高转化。 店面中内置原生实验。
- **更快的创新**：将资源从繁琐的维护中释放出来，集中精力构建提供业务价值的新功能。 使用全面的可扩展性和基于标准的技术(JavaScript、HTML、CSS和低代码工具)来构建差异化的体验。 通过单击安装第三方应用程序，以将新功能添加到您的Commerce平台。
