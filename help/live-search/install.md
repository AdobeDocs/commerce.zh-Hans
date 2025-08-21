---
title: 开始使用 [!DNL Live Search]
description: 从Adobe Commerce中了解 [!DNL Live Search] 的系统要求和安装步骤。
role: Admin, Developer
exl-id: 45b985f1-9afb-4a07-93e8-f2fe231c5400
badgePaas: label="仅限PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于云项目(Adobe管理的PaaS基础架构)和内部部署项目上的Adobe Commerce 。"
source-git-commit: 7d5e3faeef2fb16779d1558027a0b76ff3fe3a38
workflow-type: tm+mt
source-wordcount: '3138'
ht-degree: 0%

---

# 使用[!DNL Live Search]成功完成设置

Adobe Commerce [!DNL Live Search]和[[!DNL Catalog Service]](../catalog-service/guide-overview.md)共同合作，提供高性能、相关且直观的搜索解决方案，让您的客户能够快速准确地找到所需的内容。 具体来说，[!DNL Catalog Service]显示您的SaaS服务的目录数据，如要使用的[!DNL Live Search]。

本文提供了使用[!DNL Live Search]实现[!DNL Catalog Service]的分步说明。

## 受众

本文面向负责安装和配置Adobe Commerce实例的开发人员或团队中的系统集成商。

## 要求

- [Adobe Commerce](https://business.adobe.com/products/magento/magento-commerce.html) 2.4.4+
- PHP 8.1、8.2或8.3
- [!DNL Composer]
- 运行cron作业和索引器

>[!IMPORTANT]
>
>在实施[!DNL Live Search]之前，请参阅[边界和限制](boundaries-limits.md)部分以确保[!DNL Live Search]符合您的业务需求。

## 重要更新

- 截至[!DNL Live Search] 3.0.2，[!DNL Catalog Service]扩展已捆绑到安装中。

- 由于Elasticsearch 7将于2023年8月宣布终止支持，Adobe建议所有Adobe Commerce客户迁移到OpenSearch 2.x搜索引擎。 有关在产品升级期间迁移搜索引擎的信息，请参阅[升级指南](https://experienceleague.adobe.com/en/docs/commerce-operations/upgrade-guide/prepare/opensearch-migration)中的&#x200B;_迁移到OpenSearch_。

## 支持的平台

- Adobe Commerce on Cloud (ECE) ：2.4.4+
- Adobe Commerce内部部署(EE) ：2.4.4+

## 工作流概述

从较高层面来看，加入[!DNL Live Search]要求您：

1. [安装](#1-install-the-live-search-extension) [!DNL Live Search]扩展
1. [配置](#2-configure-api-keys) API密钥
1. [同步](#3-sync-your-catalog-data)您的目录数据
1. [验证](#4-verify-that-the-data-was-exported)是否已导出目录数据
1. [配置](#5-configure-the-data)数据
1. [测试](#6-test-the-connection)连接
1. [验证](#7-validate-events-are-capturing-data)事件是否正在捕获数据
1. [自定义](#8-customize-for-your-storefront)您的店面

## 1.安装[!DNL Live Search]扩展

[!DNL Live Search]是通过[Composer](https://commercemarketplace.adobe.com/magento-live-search.html)从[Adobe Marketplace](https://getcomposer.org/)安装为扩展的。 安装和配置[!DNL Live Search]后，Adobe [!DNL Commerce]开始与SaaS服务共享搜索和目录数据。 此时，*管理员*&#x200B;用户可以设置、自定义和管理搜索Facet、同义词和促销规则。

>[!BEGINTABS]

>[!TAB 新Commerce实例]

如果您在新的Commerce实例上安装[!DNL Live Search]，请按照以下说明操作。

1. 确认[cron作业](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs)和[索引器](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management)正在运行。

1. 使用Composer将Live Search模块添加到您的项目中：

   ```bash
   composer require magento/live-search --no-update
   ```

1. 更新依赖项并安装扩展：

   ```bash
   composer update magento/live-search --with-dependencies
   ```

1. 暂时禁用[!DNL OpenSearch]和相关模块，并安装[!DNL Live Search]。

   ```bash
   bin/magento module:disable Magento_ Magento_Elasticsearch8 Magento_Elasticsearch7 Magento_OpenSearch Magento_ElasticsearchCatalogPermissions Magento_InventoryElasticsearch Magento_ElasticsearchCatalogPermissionsGraphQl
   ```

   [!DNL Elasticsearch]继续管理店面的搜索请求，而[!DNL Live Search]服务在后台同步目录数据和索引产品。

1. 安装更新。

   ```bash
   bin/magento setup:upgrade
   ```

1. 验证以下[索引器](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management)是否设置为“按计划更新”：

   - 产品信息源
   - 产品变型馈送
   - 目录属性信息源
   - 产品价格信息源
   - 范围网站数据馈送
   - 范围客户组数据馈送
   - 类别信息源
   - 类别权限信息源

验证索引器后，下一步是[配置API密钥](#2-configure-api-keys)。

>[!TAB 现有Commerce实例]

如果您在现有Commerce实例上安装[!DNL Live Search]，请按照以下说明操作。

1. 确认[cron作业](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs)和[索引器](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management)正在运行。

1. 使用Composer将Live Search模块添加到您的项目中：

   ```bash
   composer require magento/live-search --no-update
   ```

1. 更新依赖项并安装扩展：

   ```bash
   composer update magento/live-search --with-dependencies
   ```

1. 禁用提供店面搜索结果的[!DNL Live Search]模块。

   ```bash
   bin/magento module:disable Magento_LiveSearchAdapter Magento_LiveSearchStorefrontPopover Magento_LiveSearchProductListing
   ```

   [!DNL Elasticsearch]继续管理店面的搜索请求，而[!DNL Live Search]服务在后台同步目录数据和索引产品。

1. 安装更新。

   ```bash
   bin/magento setup:upgrade
   ```

1. 验证以下[索引器](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management)是否设置为“按计划更新”：

   - 产品信息源
   - 产品变型馈送
   - 目录属性信息源
   - 产品价格信息源
   - 范围网站数据馈送
   - 范围客户组数据馈送
   - 类别信息源
   - 类别权限信息源

1. 启用[!DNL Live Search]扩展并禁用[!DNL OpenSearch]&#x200B;(Magento Elasticsearch和OpenSearch模块)。

   ```bash
   bin/magento module:enable Magento_LiveSearchAdapter Magento_LiveSearchStorefrontPopover  Magento_LiveSearchProductListing
   ```

   ```
   bin/magento module:disable Magento_Elasticsearch Magento_Elasticsearch6 Magento_Elasticsearch7 Magento_Elasticsearch8 Magento_OpenSearch Magento_ElasticsearchCatalogPermissions Magento_InventoryElasticsearch Magento_ElasticsearchCatalogPermissionsGraphQl
   ```

   >[!NOTE]
   >
   >disable命令包含支持OpenSearch的Commerce模块的列表。 如果您的Commerce实例未安装模块，您将看到`module does not exist`错误。

1. 安装更新。

   ```bash
   bin/magento setup:upgrade
   ```

验证索引器后，下一步是[配置API密钥](#2-configure-api-keys)。

>[!ENDTABS]

### 安装[!DNL Live Search]测试版

>[!IMPORTANT]
>
>以下功能处于测试阶段。 要参与测试版，请向[commerce-storefront-services](mailto:commerce-storefront-services@adobe.com)发送电子邮件请求。

此测试版支持[`productSearch`查询](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/)中的三种新功能：

- **分层搜索** — 在另一个搜索上下文中搜索 — 使用此功能，您最多可以为搜索查询执行两层搜索。 例如：

   - **第1层搜索** — 在“product_attribute_1”上搜索“motor”
   - **第2层搜索** — 在“product_attribute_2”上搜索“部件号123”。 此示例在结果中搜索“motor”的“部件号123”。

  分层搜索可用于`startsWith`搜索索引和`contains`搜索索引，如下所述：

- **startsWith搜索索引** — 使用`startsWith`索引进行搜索。 此新功能允许：

   - 搜索属性值以特定字符串开头的产品。
   - 配置“结尾为”搜索，以便购物者可以搜索属性值以特定字符串结尾的产品。 要启用“结束于”搜索，需要反向摄取产品属性，并且API调用也应该是一个反向字符串。

- **包含搜索索引** — 使用包含索引搜索属性。 此新功能允许：

   - 在较大的字符串中搜索查询。 例如，如果购物者搜索字符串“HAPE-123”中的产品编号“PE-123”。

     >[!NOTE]
     >
     >此搜索类型不同于现有的[短语搜索](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#phrase)，后者执行自动完成搜索。 例如，如果您的产品属性值为“outdoor pants”，则短语搜索会返回“out pan”的响应，但不会返回“oor ants”的响应。 但是，包含搜索会返回“或蚂蚁”的响应。

这些新条件增强了搜索查询过滤机制以细化搜索结果。 这些新条件不会影响主搜索查询。

您可以在搜索结果页面上实施这些新条件。 例如，您可以在页面上添加新部分，购物者可以进一步细化其搜索结果。 您可以允许购物者选择特定的产品属性，如“制造商”、“部件号”和“说明”。 从该位置，他们使用`contains`或`startsWith`条件在这些属性中搜索。 有关可搜索的[属性](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/attributes-input-types)的列表，请参阅管理员指南。

1. 要安装测试版，请将以下依赖关系添加到您的项目中：

   ```bash
   composer require magento/module-live-search-search-types:"^1.0.0-beta1"
   ```

1. 提交更改并将更改推送到`composer.json`和`composer.lock`云项目。 [了解详情](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure-store/extensions#upgrade-an-extension)。

   此测试版在管理员中为&#x200B;**[!UICONTROL Search types]**、**[!UICONTROL Autocomplete]**&#x200B;和&#x200B;**[!UICONTROL Contains]**&#x200B;添加&#x200B;**[!UICONTROL Starts with]**&#x200B;复选框。 它还更新了[`productSearch`](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-using-search-capability) GraphQL API以包含这些新搜索功能。

1. 在管理员中，[将产品属性](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/product-attributes-add#step-5-describe-the-storefront-properties)设置为可搜索，并指定该属性的搜索功能，如&#x200B;**包含**（默认值）或&#x200B;**开头为**。 您最多可以为&#x200B;**Contains**&#x200B;指定6个要启用的属性，为&#x200B;**Starts with**&#x200B;指定6个要启用的属性。 对于测试版，请注意，管理员不强制执行此限制，但会在API搜索中强制执行。

   ![指定搜索功能](./assets/search-filters-admin.png)

1. 请参阅[开发人员文档](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-using-search-capability)，了解如何使用新的[!DNL Live Search]和`contains`搜索功能更新`startsWith` API调用。

### 字段描述

| 字段 | 描述 |
|--- |--- |
| `Autocomplete` | 默认启用，无法修改。 通过`Autocomplete`，您可以在`contains`搜索筛选器[中使用](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering)。 此处，`contains`中的搜索查询返回自动完成类型的搜索响应。 Adobe建议您使用此类型的搜索来搜索描述字段，这些字段的长度通常超过50个字符。 |
| `Contains` | 启用真正的“字符串中包含的文本”搜索，而不是自动完成搜索。 在`contains`搜索筛选器[中使用](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-using-search-capability)。 有关详细信息，请参阅[限制](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#limitations)。 |
| `Starts with` | 以特定值开头的查询字符串。 在`startsWith`搜索筛选器[中使用](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-using-search-capability)。 |

## 2.配置API密钥

需要Adobe Commerce API密钥及其关联的私钥才能将[!DNL Live Search]连接到Adobe Commerce的安装。 API密钥在[!DNL Commerce]许可证持有者的帐户中生成和维护，该持有人可以与开发人员或系统集成商共享它。 然后，开发人员可以代表许可证持有人创建和管理SaaS数据空间。 如果您已经有一组API密钥，则无需重新生成它们。

请参阅[Commerce Services Connector](../landing/saas.md)文章以了解如何配置API密钥。

## 3.同步您的目录数据

[!DNL Live Search]将目录数据移动到Adobe的SaaS基础架构。 数据被编入索引，搜索结果从此索引直接传送到店面。 根据大小和复杂性，索引可能需要30分钟到几个小时。

要开始将目录数据初始同步到SaaS服务，请按照以下顺序运行以下命令：

```bash
bin/magento saas:resync --feed productattributes
bin/magento saas:resync --feed products
bin/magento saas:resync --feed scopesCustomerGroup
bin/magento saas:resync --feed scopesWebsite
bin/magento saas:resync --feed prices
bin/magento saas:resync --feed productoverrides
bin/magento saas:resync --feed variants
bin/magento saas:resync --feed categories
bin/magento saas:resync --feed categoryPermissions
```

运行这些命令时，将开始将目录数据与SaaS服务进行初始同步。

>[!WARNING]
>
>在同步过程中，搜索和类别浏览操作不可用。 该过程可能需要1小时以上的时间，具体取决于目录大小。

### 监视器同步进度

使用[数据管理仪表板](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard)监视同步进度。 此仪表板提供关于您店面产品数据的可用性的宝贵见解，确保可以及时向客户显示这些数据。

![数据管理仪表板](assets/data-management-dashboard.png)

您还可以运行sync命令，并使用[Commerce CLI](../data-export/data-export-cli-commands.md#troubleshooting)和数据导出扩展日志对同步过程进行疑难解答。

#### 将来的产品更新

初始同步后，增量产品更新最多可能需要15分钟才能用于店面搜索。 若要了解详细信息，请参阅“索引”文档中的[流式产品更新](indexing.md)。

## 4.验证是否已导出数据

要检查您的目录数据是否已从Adobe Commerce导出并与[!DNL Live Search]同步，您有几个选项：

- 在以下表中查找条目：

   - `cde_products_feed`
   - `cde_product_attributes_feed`

  >[!NOTE]
  >
  >如果您收到`table does not exist`错误，请在`catalog_data_exporter_products`和`catalog_data_exporter_product_attributes`表中查找条目。 这些表名称在4.2.1之前的[!DNL Live Search]版本中使用。

- 使用带有默认查询的[GraphQL游乐场](https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-admin/graphql)&#x200B;(有关更多详细信息，请参阅[GraphQL引用](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/))来验证以下内容：

   - 返回的产品计数接近您对商店视图的预期。
   - 将返回Facet。

有关其他帮助，请参阅支持知识库中的[[!DNL Live Search] 目录未同步](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-catalog-data-sync)。

## 5.配置数据

正确配置产品数据可确保为您的客户获得良好的搜索结果。 在此部分中，您可以启用产品列表构件并分配类别。

### 启用产品列表小组件

安装[!DNL Live Search] 4.0.0+时，默认启用产品列表小组件。 启用小组件后，会为搜索结果和类别浏览产品列表页面使用不同的UI组件。 此UI组件直接调用[目录服务API](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/)，这将缩短响应时间。

如果您的[!DNL Live Search]版本低于4.0.0+，则必须手动启用产品列表小组件。

1. 从&#x200B;*管理员*，转到&#x200B;**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**。
1. 在&#x200B;**[!UICONTROL Live Search]**&#x200B;下，选择&#x200B;**[!UICONTROL Storefront Features]**。
1. 将&#x200B;**[!UICONTROL Enable Product Listing Widgets]**&#x200B;设置为`Yes`。

   ![启用产品列表小组件](assets/ls-admin-enable-widget.png)

更改此配置时，将显示消息`Page cache is invalidated`。 您需要刷新Magento缓存以保存更改。

1. 通过执行以下操作之一访问[缓存管理](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/cache-management)页：

   - 单击工作区上方消息中的&#x200B;**[!UICONTROL Cache Management]**&#x200B;链接。
   - 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL System]** > _[!UICONTROL Tools]_>**[!UICONTROL Cache Management]**。

1. 选择&#x200B;**配置** [!UICONTROL Cache Type]并单击&#x200B;**[!UICONTROL Flush Magento Cache]**。

   刷新缓存后，立即对店面进行更改。

### 分配类别

[!DNL Live Search]中返回的产品必须分配给[类别](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/categories/categories)。 例如，在Luma中，产品被划分为“男性”、“女性”和“齿轮”等类别。 “Top”、“Bottoms”和“Watches”也设置了子类别。 这些类别分配可改进筛选时的粒度。

## 6.测试连接

现在，在SaaS中使用目录数据，测试以确保在以下情况下返回产品数据：

- [!UICONTROL Search]框正确返回结果
- 类别浏览正确返回结果
- Facet在搜索结果页面上可用作过滤器

如果一切工作正常，[!DNL Live Search]已安装、连接并可以使用。

如果在店面中遇到问题，请检查`var/log/system.log`文件中是否有服务端的API通信失败或错误。

要允许[!DNL Live Search]通过防火墙，请将`commerce.adobe.io`添加到允许列表。

## 7.验证事件是否正在捕获数据

确保部署到您站点的店面事件正常工作。 此检查对于Headless实施尤其重要。

- 查看[所需的](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#live-search)事件[!DNL Live Search]。
- 确保[实时搜索仪表板](performance.md)显示的是来自非生产环境的数据。
- [验证事件集合](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/verify/)。

## 8.针对您的店面进行定制

您已安装[!DNL Live Search]扩展、同步、验证和配置您的数据。 下一步是确保[!DNL Live Search]构件符合商店的外观。

您可以根据需要通过定义自定义CSS规则来设置弹出框和PLP小组件的样式。 查看[样式弹出框元素](storefront-popover.md#styling-popover-example)和[产品列表页小组件](plp-styling.md#styling-example)。

如果您希望扩展小组件的功能，则每个小组件的源代码在公共存储库中可用。
在此方案中，您可以根据自己的需求自定义JavaScript，然后将自定义代码托管在您的CDN上。 此自定义脚本与[!DNL Live Search]服务通信并返回正常结果，从而允许您控制小组件的功能。

- [PLP Widget存储库](https://github.com/adobe/storefront-product-listing-page)
- [搜索栏存储库](https://github.com/adobe/storefront-search-as-you-type)

## 正在更新[!DNL Live Search]

在更新[!DNL Live Search]之前，请检查使用编辑器安装的[!DNL Live Search]版本。

```bash
composer show magento/module-live-search | grep version
```

要更新[!DNL Live Search]，请从命令行运行以下命令：

```bash
composer update magento/live-search --with-dependencies
```

要更新到主要版本，例如从3.1.1到4.0.0，请按如下方式编辑项目的根[!DNL Composer] `.json`文件：

1. 如果当前安装的`magento/live-search`版本为`3.1.1`或更低版本，并且要升级到版本`4.0.0`或更高版本，请在升级之前运行以下命令：

   ```bash
   bin/magento module:enable Magento_AdvancedSearch
   ```

   有关当前安装的`magento/live-search`版本的信息，请运行以下命令：

   ```bash
   composer show magento/live-search
   ```

1. 打开根`composer.json`文件并搜索`magento/live-search`。

1. 在`require`部分中，更新版本号，如下所示：

   ```json
   "require": {
      ...
      "magento/live-search": "^4.0",
      ...
    }
   ```

1. 保存`composer.json`。 然后，从命令行运行以下命令：

   ```bash
   composer update magento/live-search --with-dependencies
   ```

## 正在卸载[!DNL Live Search]

要卸载[!DNL Live Search]，请参阅[卸载模块](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/uninstall-modules)。

## [!DNL Live Search]包

[!DNL Live Search]扩展包含以下包：

| 包 | 描述 |
|--- |--- |
| `module-live-search` | 允许商家配置其针对分面、同义词、查询规则等的搜索设置，并提供对只读GraphQL游乐场的访问权限，以测试来自&#x200B;*管理员*&#x200B;的查询。 |
| `module-live-search-adapter` | 将搜索请求从店面路由到[!DNL Live Search]服务，并在店面中呈现结果。 <br /> — 类别浏览 — 将请求从店面[顶部导航](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/navigation/navigation-top)路由到搜索服务。<br /> — 全局搜索 — 将请求从[快速搜索](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search)字段路由到[!DNL Live Search]服务。 快速搜索字段位于店面页面的右上角。 |
| `module-live-search-storefront-popover` | “键入时搜索”弹出框取代了标准快速搜索，并返回排名最前的搜索结果的数据和缩略图。 |

## [!DNL Live Search]依赖项

用于安装[!DNL Composer]扩展的[!DNL Live Search]中继包包括以下模块依赖项。

- `magento/module-saas-catalog`
- `magento/module-saas-category`
- `magento/module-saas-category-permissions`
- `magento/module-saas-product-override`
- `magento/module-saas-product-variant`
- `magento/module-saas-price`
- `magento/module-saas-scopes`
- `magento/module-bundle-product-data-exporter`
- `magento/module-catalog-inventory-data-exporter`
- `magento/module-catalog-url-rewrite-data-exporter`
- `magento/module-configurable-product-data-exporter`
- `magento/module-parent-product-data-exporter`
- `magento/module-gift-card-product-data-exporter`
- `magento/module-bundle-product-override-data-exporter`
- `data-services`
- `services-id`

## 高级概念

以下部分提供了使用[!DNL Live Search]和[!DNL Catalog Service]时更高级的主题。

### 端点

[!DNL Live Search]通过`https://catalog-service.adobe.io/graphql`处的端点进行通信。

由于[!DNL Live Search]没有访问完整产品数据库的权限，[!DNL Live Search] GraphQL和Commerce核心GraphQL API没有完全奇偶校验。

Adobe建议直接调用SaaS API，尤其是目录服务端点。

- 通过绕过Commerce数据库/Graphql进程来提高性能并降低处理器负载
- 利用[!DNL Catalog Service]联盟从单个终结点调用[!DNL Live Search]、[!DNL Catalog Service]和[!DNL Product Recommendations]。

对于某些用例，调用[!DNL Catalog Service]以获取产品详细信息和类似用例可能更好。 有关详细信息，请参阅[refineProduct](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/)。

如果您有自定义Headless实施，请查看[!DNL Live Search]引用实施：

- [PLP小组件](https://github.com/adobe/storefront-product-listing-page)
- [[!DNL Live Search] 字段](https://github.com/adobe/storefront-search-as-you-type)

默认情况下，如果您未使用搜索适配器、Luma构件或AEM CIF构件等标准组件，则自动收集用户交互数据将不起作用。 Adobe Sensei将使用此收集的数据进行智能推销和性能跟踪。 要解决此问题，您需要开发自定义解决方案，以采用Headless方式实施此数据收集。

[!DNL Live Search]的最新版本已使用[!DNL Catalog Service]。

### 语言支持

[!DNL Live Search]小组件支持以下语言：

|  |  |  |  |
|--- |--- |--- |--- |
| 语言 | 区域 | 语言代码 | Magento区域设置 |
| 保加利亚语 | 保加利亚 | bg_BG | bg_BG |
| 加泰罗尼亚语 | 西班牙 | ca_ES | ca_ES |
| 捷克语 | 捷克共和国 | cs_CZ | cs_CZ |
| 丹麦语 | 丹麦 | da_DK | da_DK |
| 德语 | 德国 | de_DE | de_DE |
| 希腊语 | 希腊 | el_GR | el_GR |
| 英语 | 英国 | en_GB | en_GB |
| 英语 | 美国 | en_US | en_US |
| 西班牙语 | 西班牙 | es_ES | es_ES |
| 爱沙尼亚语 | 爱沙尼亚 | et_EE | et_EE |
| 巴斯克语 | 西班牙 | eu_ES | eu_ES |
| 波斯语 | 伊朗 | fa_IR | fa_IR |
| 芬兰语 | 芬兰 | fi_FI | fi_FI |
| 法语 | 法国 | fr_FR | fr_FR |
| 加利西亚语 | 西班牙 | gl_ES | gl_ES |
| 印地语 | 印度 | hi_IN | hi_IN |
| 匈牙利语 | 匈牙利 | hu_HU | hu_HU |
| 印尼语 | 印度尼西亚 | id_ID | id_ID |
| 意大利语 | 意大利 | it_IT | it_IT |
| 朝鲜语 | 韩国 | ko_KR | ko_KR |
| 立陶宛语 | 立陶宛 | lt_LT | lt_LT |
| 拉脱维亚语 | 拉脱维亚 | lv_LV | lv_LV |
| 挪威语 | 挪威博克马尔语 | nb_NO | nb_NO |
| 荷兰语 | 荷兰 | nl_NL | nl_NL |
| 波兰语 | 波兰 | pl_PL | pl_PL |
| 葡萄牙语 | 巴西 | pt_BR | pt_BR |
| 葡萄牙语 | 葡萄牙 | pt_PT | pt_PT |
| 罗马尼亚语 | 罗马尼亚 | ro_RO | ro_RO |
| 俄语 | 俄罗斯 | ru_RU | ru_RU |
| 瑞典语 | 瑞典 | sv_SE | sv_SE |
| 泰语 | 泰国 | th_TH | th_TH |
| 土耳其语 | 土耳其 | tr_TR | tr_TR |
| 中文 | 中国 | zh_CN | zh_Hans_CN |
| 中文 | 台湾 | zh_TW | zh_Hant_TW |

如果构件检测到Commerce管理语言设置与支持的语言匹配，则它会默认为该语言。 否则，小组件将默认使用英语。 在Admin中，通过导航到&#x200B;_[!UICONTROL Stores]_> [!UICONTROL Settings] >_[!UICONTROL Configuration]_ > _[!UICONTROL General]_> [!UICONTROL Country Options]来配置语言设置。

管理员还可以设置[搜索索引](settings.md#language)的语言，以帮助确保获得更好的搜索结果。

### 构件代码存储库

产品列表页面构件和[!DNL Live Search]字段构件的代码可从GitHub下载。

有权访问代码的开发人员可以完全自定义代码的工作方式和外观。 他们在自己的服务器上托管代码，但仍使用[!DNL Live Search]服务。

- [PLP小组件](https://github.com/adobe/storefront-product-listing-page)
- [搜索栏](https://github.com/adobe/storefront-search-as-you-type)

### Data Export扩展

启用[!DNL Live Search]后，Data Export扩展将在Commerce应用程序和[!DNL Live Search]之间同步Commerce数据。 此过程确保店面上有最新的Commerce数据。 在Admin中，您可以使用数据管理功能板检查同步状态。 您可以使用Commerce CLI和日志管理数据导出过程并排除其故障。 有关详细信息，请参阅[数据导出指南](../data-export/overview.md)。

### Inventory management

[!DNL Live Search]支持Commerce中的[Inventory management](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/introduction)功能(以前称为多Source清单，或MSI)。 要启用完全支持，您必须[将](install.md#updating-live-search)依赖项模块`commerce-data-export`更新为版本102.2.0+。

[!DNL Live Search]返回一个布尔值，表明产品在Inventory management中是否可用，但不包含有关哪个来源具有库存的信息。

### 价格索引器

[!DNL Live Search]客户可以使用[SaaS价格索引器](../price-index/price-indexing.md)，它提供了更快的价格更改更新和同步时间。

### 价格支持

[!DNL Live Search]小组件支持Adobe Commerce支持的大多数（但不是所有）价格类型。

目前支持基本价格。 不受支持的高级价格包括：

- 成本
- 最低广告价格

查看[API Mesh](../catalog-service/mesh.md)以了解更复杂的价格计算。

价格格式支持Commerce实例中的区域设置配置设置： *存储* >设置> *配置* >常规> *常规* >本地选项>区域设置。

### Headless店面支持

（可选）您可能需要安装`module-data-services-graphql`模块，该模块扩展了应用程序的现有GraphQL覆盖范围，以包含店面行为数据收集所需的字段。

```bash
composer require magento/module-data-services-graphql
```

此模块可向GraphQL查询添加其他上下文：

- `dataServicesStorefrontInstanceContext`
- `dataServicesMagentoExtensionContext`
- `dataServicesStoreConfigurationContext`

### B2B支持

[!DNL Live Search]支持[B2B功能](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/guide-overview)及其他[限制](boundaries-limits.md#b2b-and-category-permissions)。

### PWA支持

[!DNL Live Search]适用于PWA Studio，但用户可能会看到与其他Commerce实施相比的细微差异。 在威尼亚省可以使用搜索和产品列表页面等基本功能，但Graphql的某些排列可能无法正常工作。 此外，可能存在性能差异。

- 与使用本机PWA店面的[!DNL Live Search]相比，当前[!DNL Live Search]的Commerce实现需要更多的处理时间来返回搜索结果。
- PWA中的[!DNL Live Search]不支持[事件处理](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/)。 因此，搜索报表和智能促销在PWA商店中不起作用。
- 使用[PWA Studio](https://developer.adobe.com/commerce/pwa-studio/)时，GraphQL不支持直接筛选`description`、`name`、`short_description`，但是这些字段可以通过更一般的筛选器返回。

要将[!DNL Live Search]与PWA Studio结合使用，集成商还必须：

1. 安装[livesearch-storefront-utils](https://www.npmjs.com/package/@magento/ds-livesearch-storefront-utils)。
1. 在`environmentId`对象中设置`storeDetails`。

   ```javascript
   const storeDetails: StoreDetailsProps = {
       environmentId: <Storefront_ID>,
       websiteCode: "base",
       storeCode: "main_website_store",
       storeViewCode: "default",
       searchUnitId: searchUnitId,
       config: {
           minQueryLength: 5,
           pageSize: 8,
           currencySymbol: "$",
           },
       };
   ```

### Cookies

[!DNL Live Search]收集用户交互数据，作为其基本功能的一部分，Cookie用于存储此数据。 在收集任何用户信息时，用户必须同意存储Cookie。 [!DNL Live Search]和[!DNL Product Recommendations]共享数据流，因此使用相同的Cookie机制。 有关它的详细信息，请参阅[句柄Cookie限制](https://experienceleague.adobe.com/en/docs/commerce/product-recommendations/developer/setting-cookie)。
