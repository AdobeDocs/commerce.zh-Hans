---
title: 适用于Commerce的Adobe Commerce Optimizer Connector
description: 了解如何将Commerce云或内部部署项目中的数据连接到Adobe Commerce Optimizer
feature: Personalization, Integration, Configuration
badgePaas: label="仅限PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于云项目(Adobe管理的PaaS基础架构)和内部部署项目上的Adobe Commerce 。"
hidefromtoc: true
hide: true
source-git-commit: 36cfafff243a2310a17a2c9ec8a00f10403bc133
workflow-type: tm+mt
source-wordcount: '1552'
ht-degree: 0%

---


# 适用于Commerce的Adobe Commerce Optimizer Connector

Adobe Commerce Connector是一座集成桥，用于在云或本地部署的现有Adobe Commerce Cloud与Adobe Commerce Optimizer可组合目录数据模型之间同步目录和定价数据。 此功能支持诸如动态AI搜索、推荐、快速加载Headless商店前台(包括Edge Delivery Services上的Adobe Commerce商店前台)和实时性能分析等功能。

>[!NOTE]
>
>本文档描述了早期访问开发中的产品，并未反映用于正式发布的所有功能。

## 架构和体验

Adobe Commerce Connector通过将Commerce的`website/store/storeview`目录层次结构映射到Adobe Commerce Optimizer `channel/policy/source`数据模型来操作。

您可以使用[Commerce促销工具](../optimizer/merchandising/overview.md)管理产品发现(Live Search)和推荐（产品推荐）规则配置，而不是通过Commerce管理员来配置和管理Adobe Commerce Optimizer服务（Live Search和产品推荐）。  Adobe Commerce实例将成为目录和价格数据的数据源。 在Commerce中更新数据时，更新将同步到Adobe Commerce Optimizer实例。

## 工作流

连接器支持多个关键工作流：

* **将Commerce目录数据导出到Adobe Commerce Optimizer** — 在`website`级别上导出价格和价格手册数据。 产品和产品属性数据在`store view`级别导出。 默认情况下，所有Commerce作用域（网站和商店视图）的目录数据同步处于启用状态。

  要启用此工作流，请使用编辑器安装`adobe-commerce/commerce-data-export-aco-adapter` PHP扩展，然后提供IMS凭据来验证Commerce项目之间的连接。

* **映射Commerce `website/store/storeview`数据以导出到Adobe Commerce Optimizer**

  您可以通过从管理员(**[!UICONTROL Stores]** -> [!UICONTROL Settings] -> **[!UICONTROL All Stores]**)中的存储网格更新导出程序配置，选择自定义Adobe Commerce Optimizer导出程序设置以仅导出特定作用域的数据。

* **促销规则配置和管理**

  启用连接器后，将从Adobe Commerce Optimizer UI而不是从Commerce管理员的[!UICONTROL Live Search]和[!UICONTROL Product Recommendations]页面定义和管理产品发现和推荐的促销规则。

* **在Edge Delivery Services上部署您的Commerce店面**

  设置与Adobe Commerce Optimizer的集成后，您可以在Edge Delivery服务上设置和部署Commerce店面，以使用Adobe Commerce Optimizer提供的可组合、API驱动的架构和模块化组件提供超快的性能、可扩展性、无缝的内容创作、集成的个性化并降低运营成本。

## 使用该集成的要求

* Adobe Commerce 2.4.5+

   * PHP 8.1、8.2、8.3或8.4
   * Composer 2.x

* 带有已配置沙盒实例的Adobe Commerce Optimizer许可证。

* 访问[repo.magento.com](https://repo.magento.com)以使用Composer下载Commerce连接器中继包。

* 管理员访问[Adobe Commerce Optimizer沙盒实例](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-commerce-optimizer/create-first-instance)。

配置集成的Adobe Commerce用户必须具有：

* Adobe Commerce管理员的管理员访问权限。

* [对Adobe Commerce应用程序服务器的命令行访问权限](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/project/user-access)。

* 开发人员对配置了Adobe Commerce Optimizer项目的[IMS组织](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations?)的访问权限。

## 开始使用

1. **设置集成**

   1. [安装Commerce连接器包](#install-the-commerce-connector-package)。

   1. [获取配置Commerce Optimizer连接所需的值](#get-required-values-for-configuring-the-commerce-optimizer-connection)

   1. [启用Adobe Commerce Optimizer集成](#enable-the-adobe-commerce-optimizer-integration)。

   1. [验证数据同步是否正常工作](#verify-that-the-data-sync-is-working)。

   1. [自定义数据导出配置](#customize-commerce-data-export-configuration)（可选）。

1. **[配置Adobe Commerce Optimizer商店](#configure-adobe-commerce-optimizer-stores)**

1. **[在Edge Delivery Services上设置Commerce店面](#set-up-a-commerce-storefront-on-edge-delivery-services)**

## 安装Commerce连接器软件包

所有具有Adobe Commerce活动许可证的Commerce商家都可使用Adobe Commerce Optimizer连接器编辑器中继包。

### 安装步骤

1. 使用编辑器添加`adobe-commerce/commerce-data-export-aco-adapter`模块：

```shell
 composer require adobe-commerce/commerce-data-export-aco-adapter
```

1. 将更改部署到Adobe Commerce暂存环境。

部署更改后，Commerce Optimizer Optimizer选项在Commerce的“管理员”菜单中可用。

>[!NOTE]
>
>有关详细的扩展安装说明，请参阅以下指南：
>
>在云基础架构上的Adobe Commerce上[安装扩展](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure-store/extensions)
>
>[在本地安装Adobe Commerce扩展](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/extensions)

## 获取配置Commerce Optimizer连接所需的值

### 获取API凭据

>[!NOTE]
>
>如果您在部署了App Builder实例的IMS组织中已经拥有Commerce Optimizer开发人员项目，则可以从该项目中的OAUTH服务器到服务器凭据中获取所需的API凭据和组织ID。

在Adobe Developer控制台中新建一个开发人员项目，以获取API凭据来配置Commerce与Commerce Optimizer实例之间的集成。 有关说明，请参阅开发人员文档中的[创建App Builder项目](https://developer.adobe.com/commerce/extensibility/events/project-setup/)。

创建项目后，从“OAUTH服务器到服务器身份证明”页中保存以下值：

* **组织ID** (`org_id`)

* **IMS `client_id`和`client_secret`**

### 获取Adobe Commerce Optimizer实例详细信息

从Adobe Commerce Optimizer实例详细信息中保存以下值。

* **实例ID - **您的Adobe Commerce Optimizer实例的唯一标识符。 也称为租户ID。

  从URL获取实例ID以访问您的Adobe Commerce Optimizer实例。 例如，在URL `https://na1-sandbox.admin.commerce.adobe.com/1234567890abcdef`中，实例ID为`1234567890abcdef`。

* **区域 — **托管Adobe Commerce Optimizer沙盒实例的区域。

  从Adobe Commerce Optimizer URL获取区域。 例如，在URL `https://na1-sandbox.admin.commerce.adobe.com/1234567890abcdef`中，区域是`na1`。

## 启用Adobe Commerce Optimizer集成

>[!IMPORTANT]
>
>运行配置命令时，数据同步处理会启动。 默认情况下，所有Commerce作用域（网站和商店视图）的目录数据同步处于启用状态。 根据目录的大小，数据同步过程可能需要几个小时。

使用您在上一步中收集的API凭据和实例详细信息，您现在可以配置Commerce实例与Adobe Commerce Optimizer实例之间的集成。

1. 从Commerce Admin中，选择&#x200B;**[!UICONTROL Adobe Commerce Optimizer]**&#x200B;以显示包含说明的配置页面。

   ![Adobe Commerce Optimizer配置页面](../assets/aco-connector-config-page.png)

1. 从命令行中，[使用SSH](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/secure-connections)连接到Commerce暂存环境。

1. 运行以下Commerce CLI命令配置集成，将占位符值替换为Commerce Optimizer项目的值：

```terminal
bin/magento aco:config:init --org_id=<<your_org_id>> --tenant_id=<<your_tenant_id>> --client_id=<<your_client_id>> --client_secret=<<your_client_secret>> --region=<<na1>> --type=sandbox
```

1. 通过返回Commerce管理员并选择[!UICONTROL Adobe Commerce Optimizer]选项来验证连接。

   单击该选项后，它将在新选项卡中打开Adobe Commerce Optimizer UI。

## 验证数据同步是否正常工作

您可以从Commerce管理员和Commerce Optimizer中检查数据同步。

* **[数据馈送同步状态页面](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status.md)**&#x200B;显示从Commerce到Adobe Commerce Optimizer的目录数据同步进度。

* Adobe Commerce Optimizer中的&#x200B;**[[!UICONTROL Data Sync]页面](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/data-sync)**&#x200B;显示从Commerce实例传输的目录数据。

1. 验证目录数据是否从Commerce流向Commerce Optimizer：

   从Commerce管理员中，选择[!UICONTROL Data Feed Sync Status]** > [!UICONTROL System] > [!UICONTROL Data Transfer]以打开&#x200B;**[!UICONTROL Data Feed Sync Status]**&#x200B;页面。

   ![带有馈送项状态报告的数据馈送同步状态页面](./assets/data-feed-sync-status.png)

   如果数据同步已启动，则馈送数据将显示已成功发送的记录。 您还可以通过查看每个馈送的详细信息来查看和解决同步问题。

1. 验证Adobe Commerce Optimizer是否正在接收目录数据：

   从Commerce Optimizer菜单中，选择&#x200B;**[!UICONTROL Data Sync]**&#x200B;以打开“数据同步”页面。

   ![数据同步](./assets/data-sync.png)

### 故障排除

如果数据同步尚未启动，请确保目录索引有效。 如果索引无效，请从Commerce CLI运行以下命令以重新索引目录数据：

```terminal
bin/magento indexer:reindex" catalog indexer re-index CLI command to start PaaS to ACO catalog data synchronization.
```

## 自定义Commerce数据导出配置

您可以通过从管理员(**[!UICONTROL Stores]** -> [!UICONTROL Settings] -> **[!UICONTROL All Stores]**)中的存储网格更新导出程序配置，选择自定义Adobe Commerce Optimizer导出程序设置以仅导出特定作用域的数据。

* 在`website`级别，禁用导出程序设置将停止将价格和价格手册数据导出到Adobe Commerce Optimizer。

* 在`storeview`级别，禁用导出器设置将停止将产品和产品属性导出到Adobe Commerce Optimizer。

当配置改变时，相应的索引失效，以触发受影响实体的再导出。

## 配置Adobe Commerce Optimizer商店

通过创建目录视图和策略来配置Adobe Commerce Optimizer存储。&#x200B; 请参阅Adobe Commerce Optimizer指南中的[创建目录视图](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/catalog-view)。

请注意，价格手册是自动从Adobe Commerce客户组创建的。

## 在Edge Delivery Services上设置Commerce店面

本节简要介绍设置Commerce店面所需的步骤。 有关详细信息，请参阅[Adobe Commerce店面] (https://experienceleague.adobe.com/developer/commerce/storefront/)文档网站。

1. 使用[站点创建者工具](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator)将Adobe Commerce店面模板克隆并部署到EDS。

1. [设置本地开发环境](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/#set-up-local-environment)。

1. [安装GraphQL Storefront兼容包](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility/install/)。&#x200B;

1. [在云环境中为Commerce实例配置CORS标头](#configure-cors-headers-for-commerce-instance)。

1. [将店面连接到Commerce数据源](#connect-the-storefront-to-commerce-data-sources)。

### 为Commerce实例配置CORS标头

要允许GraphQL请求从Edge Delivery Services (EDS)店面发送到云或本地环境中的Adobe Commerce，请使用以下选项之一将特定的跨源资源共享(CORS)标头添加到Adobe Commerce GraphQL端点&#x200B;。

1. 将跨源资源共享(CORS)标头添加到Adobe Commerce GraphQL端点&#x200B;。

   **选项1：为Adobe Commerce foundation实施PHP自定义模块，以便能够添加CORS标头。&#x200B;**

   **选项2：安装第三方社区模块graycore/magento2-cors&#x200B;** — 请参阅[Adobe Commerce店面](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/cors-setup/)文档中的&#x200B;*CORS设置*。

1. 将以下CORS变量添加到云实例`app.yaml`环境配置文件上的Commerce：

   * `CONFIG__DEFAULT__WEB__GRAPHQL__CORS_ALLOWED_HEADERS: *`
   * `CONFIG__DEFAULT__WEB__GRAPHQL__CORS_ALLOWED_ORIGINS: *`

### 将店面连接到Commerce数据源

在Storefront样板代码的GitHub存储库中，使用以下参数更新店面配置文件`config.json`：

* `"commerce-core-endpoint": "Commerce cloud instance GraphQL endpoint"`

* `"commerce-endpoint": "Commerce Optimizer instance GraphQL endpoint"` — 从[Commerce Optimizer实例详细信息页面](https://experienceleague.adobe.com/en/docs/commerce/optimizer/get-started#get-instance-details)获取此值&#x200B;

* `"AC-Environment-Id": "Customer organization ID"` — 从[Commerce云项目](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/project/overview#project-overview)中获取此值

* `"AC-View-ID": "Catalog view ID in Commerce Optimizer Admin"` — 从Adobe Commerce Optimizer管理员处获取此值。

* `"AC-Price-Book-ID": "base::b6589fc6ab0dc82cf12099d1c2d40ab994e8410c"` — 从Adobe Commerce Optimizer管理员处获取此值&#x200B;。

* `"AC-Source-Locale": "Catalog source – Store View code from Commerce cloud instance"`

有关详细信息，请参阅[Adobe Commerce店面](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/)文档中的&#x200B;*店面配置*。


