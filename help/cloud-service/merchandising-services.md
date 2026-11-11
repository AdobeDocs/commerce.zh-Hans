---
title: 可组合目录数据模型和促销服务
description: 了解可组合目录数据模型如何更改[!DNL Adobe Commerce as a Cloud Service]中的目录交付，以及商家和店面团队需要了解的信息。
feature: Catalog Management, Personalization, Saas
role: Leader
level: Beginner
autotag-review: '2026-11-09T05:07:21.124Z'
TQID: 'https://experienceleague.adobe.com/5Aaumfx9-lOBMDOg59rr-MMl-0sgFLSVUzngkdzfyR0'
product_v2:
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 22bad240-8308-569b-a9d5-578f1ff890ca
    internal-label: Customers
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 76cfaac4-e563-56dd-8938-708bf8b84956
    internal-label: Attributes
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: a8ae7a5a-6cdc-5922-bd0d-6feb44b04984
    internal-label: Upgrade
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
    internal-label: Catalog management
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
  - id: e9004f3c-09ae-5d24-acd2-fa0987fdb66e
    internal-label: Companies
  - id: f37757d8-3174-5335-b977-1161792f965d
    internal-label: Personalization
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
    internal-label: Reporting
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
source-git-commit: 0bda134570bb3bf2f43da545917dedc95394df5e
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 0%
---

# 促销服务

Adobe Commerce as a Cloud Service现在通过促销服务支持可组合目录数据模型(CCDM)。 Adobe Commerce Optimizer引入了此数据模型，CCDM为这两种产品提供了通用基础，使其可在同一基础上提供店面目录浏览和促销功能，而Commerce基金会则可继续管理产品、价格和交易。

本主题将介绍CCDM有何变化，哪些功能会持续存在，以及这种变化对商家、合作伙伴和店面开发人员意味着什么。

## CCDM会引入哪些更改？

原始目录模型使用目录服务将产品数据交付到店面，实时搜索和产品推荐提供搜索、销售和推荐功能。 在此模型中，Commerce使用[SaaS数据导出](https://experienceleague.adobe.com/zh-hans/docs/commerce/saas-data-export/overview)进行同步。

通过CCDM，这些功能与支持Adobe Commerce Optimizer的目录基础相同。 [目录视图](https://experienceleague.adobe.com/en/docs/commerce-admin/merchandising-with-ccdm/setup/catalog-view)和[策略](https://experienceleague.adobe.com/en/docs/commerce-admin/merchandising-with-ccdm/setup/policies)定义可用于店面的目录上下文。 策略决定了产品分类，并且促销规则可以应用于所有目录视图或针对特定视图进行定制。

这会更改目录的配置、访问和推销方式。 CCDM以原始Commerce目录的搜索、推荐和促销功能为基础，同时在目录视图级别引入控件。 其他管理和报告功能如下所述。

Commerce基金会仍然是产品和价格的规范来源。 产品和价格数据通过本机Adobe Commerce as a Cloud Service集成以单向方式同步到CCDM。 网站、商店和商店视图配置保留在Commerce中，以及现有的购物车、结帐和订单管理工作流。

## 许可和配置

现有Adobe Commerce as a Cloud Service SKU中包含促销服务。 它不是第二个产品或订阅，并且不需要单独的Adobe Commerce Optimizer购买、授权或租户。

## 架构概述

[!DNL Commerce Foundation]仍然是产品和价格的主要记录，并继续管理交易记录。 本机集成将产品和价格数据从[!DNL Commerce]单向同步到CCDM。 您不为此同步安装单独的连接器或[!DNL App Builder]应用。

店面使用CCDM支持的促销服务来检索目录数据和上下文，以便进行浏览、搜索、推荐和促销。 请求使用目录上下文检索针对目标受众的产品和价格。 您继续在[!DNL Commerce]中管理网站、商店和商店视图配置。

下图显示了促销服务在更广泛的Adobe Commerce as a Cloud Service架构中的位置。

![Commerce架构，显示流入促销服务的目录数据](./assets/data-flow-ccdm.png){zoomable="yes"}

## 商家有哪些新增功能？

通过新模型，您可以将现有促销规则范围限定为所有目录视图或特定视图。 这样，您就可以将促销应用于每个店面受众。 了解如何[将促销规则范围设定为目录视图](https://experienceleague.adobe.com/en/docs/commerce-admin/merchandising-with-ccdm/merchandising/rules/add)。

在Admin中，您可以使用[!UICONTROL Catalog Views]和[!UICONTROL Policies]配置目录上下文。 您还可以使用[!UICONTROL Success Metrics]查看收入、转化、参与度、客户获取和跳出率。 有关详细信息，请参阅[成功量度](https://experienceleague.adobe.com/en/docs/commerce-admin/merchandising-with-ccdm/manage-results/success-metrics)。

## 采用之前的注意事项

在采用促销服务之前，请查看CCDM模型如何影响您的许可、目录集成、店面和管理工作流。

### 目录管理和集成

继续管理[!DNL Commerce Foundation]中的产品和价格。 本机集成会将它们同步到CCDM。 请勿为Merchandising Services创建第二个产品目录。

### 店面实施

您的店面如何检索目录数据取决于您的实施：

- **[!DNL Adobe Commerce Storefront]**&#x200B;个插件 — 插件处理转换。 无需更改代码。 请参阅[storefront设置文档](https://experienceleague.adobe.com/en/tools/commerce-storefront/)。
- **自定义或其他店面** — 按照[标头配置引用](https://experienceleague.adobe.com/en/tools/commerce-storefront/setup/configuration/commerce-configuration/#headers)中的说明更新您的目录请求标头。

查看您的目录查询和请求标头，以了解基于CCDM的模型。 请勿假设现有查询或标头保持不变。 促销GraphQL查询与原始目录服务模型中使用的查询不同。 其他查询支持CCDM。 使用[推销GraphQL API引用](https://developer.adobe.com/commerce/services/reference/graphql/)并根据[店面标题引用](https://experienceleague.adobe.com/en/tools/commerce-storefront/setup/configuration/commerce-configuration/#headers)验证所需的目录上下文。

### 第三方应用程序和扩展

查看读取目录数据或使用目录事件的第三方应用程序和扩展。 兼容性取决于每个应用程序或扩展使用这些界面的方式。

### 管理体验

带有CCDM的Adobe Commerce as a Cloud Service使用[[!DNL Adobe Unified Experience]](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/start/admin/admin-unified-experience) (Unified Shell)。 Adobe独立于CCDM发布了Unified Shell。 原始目录服务模型上的现有实例保留对Classic和Unified Shell的访问权限。

### 限制

CCDM模型不会更改Adobe Commerce as a Cloud Service限制。 与Optimizer共享目录基础并不意味着Commerce会继承Optimizer容量或限制。

## 可用性和迁移

对于在此版本之后开始使用Adobe Commerce as a Cloud Service的组织，默认情况下会收到促销服务。 如果贵组织需要原始目录数据模型，请联系您的Adobe客户团队以讨论例外是否可用。

在此版本之前拥有Adobe Commerce as a Cloud Service的组织可以在[配置新实例](./getting-started.md#create-an-instance)时选择任一目录模型。 默认情况下，[!UICONTROL Enable CCDM]切换器处于禁用状态。 启用CCDM后，便无法禁用它。

现有实例不会自动更改。 在正式发布时(GA)，您不能将现有的原始目录服务实例迁移到促销服务。
