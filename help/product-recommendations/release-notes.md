---
title: '[!DNL Product Recommendations]发行说明'
description: Adobe Commerce中 [!DNL Product Recommendations] 的最新发行信息。
feature: Services, Recommendations, Release Notes
exl-id: 37404605-5b62-4c71-90d1-4f09e6105c4b
source-git-commit: ac1f3497292cc586810eb44a408f7d4d7088a96d
workflow-type: tm+mt
source-wordcount: '1820'
ht-degree: 0%

---

# [!DNL Product Recommendations]发行说明

发行说明包含以下[!DNL Product Recommendations]模块的更新：

* [!DNL Product Recommendations]中继包： `magento/product-recommendations`
* [!DNL Product Recommendations]（可选）模块中的页面生成器支持： `magento/module-page-builder-product-recommendations`
* 对[!DNL Product Recommendations] （可选）模块的视觉相似性推荐类型支持： `magento/module-visual-product-recommendations`

为最新发布的版本提供支持。 提供了旧版本的发行说明以供参考。
发行说明包括：

![新](../assets/new.svg)新功能
![修复](../assets/fix.svg)修复和改进
![错误](../assets/bug.svg)已知问题

请参阅开发人员文档，以[了解产品支持](https://experienceleague.adobe.com/zh-hans/docs/commerce-operations/release/product-availability)。

## 托管服务更新

这些说明描述了在版本化版本之外发布或发现的更新或已知问题，或对托管服务的改进。

_2025年1月31日_

![新](../assets/new.svg)测试环境中无查询的目录数据有新的数据保留策略。 [了解详情](overview.md#catalog-data-retention-policy)。

_2024年6月28日_

![错误](../assets/bug.svg)重新加载购物车页面时，从购物车页面上的[!DNL Product Recommendations]设备添加到购物车的产品不会从推荐产品列表中删除。
![错误](../assets/bug.svg)从购物车中删除的产品将继续保留在`cartSkus`阵列中，直到购物车页面重新加载为止。

_2023年7月18日_

![新](../assets/new.svg) [!DNL Product Recommendations]现在具有GraphQL [`recommendations`](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/)查询。

_2023年4月25日_

![新](../assets/new.svg) [!DNL Product Recommendations]客户现在可以使用[SaaS价格索引](../price-index/price-indexing.md)。

## 当前主要版本

### 6.4.0 magento/product-recommentations

_2025年9月17日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![修复](../assets/fix.svg)解决了本地存储数据不可用时，产品推荐单元因JavaScript错误而消失的间歇性问题。 此修复确保PREX在本地存储中缺少`ds-view-history-time-decay`时不再引发错误。
![新](../assets/new.svg)已将`recommendations-sdk`的CDN URL更新到`adobe.io`域。

### 先前版本

### 6.3.0的magento/product-recommendations

_2025年9月5日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)添加了对在[产品推荐工作区](page-builder.md)的非默认存储视图中创建的[PageBuilder推荐单元](workspace.md)的量度的显示支持。
![新](../assets/new.svg)产品推荐现在完全遵循[Cookie限制模式](setting-cookie.md)，方法是在启用限制时阻止在Cookie/本地存储中进行数据收集和存储。

### 6.2.1的magento/product-recommendations

_2025年7月14日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![修复](../assets/fix.svg)对[预览推荐](./create.md#preview-recommendations)面板进行了改进。

### 6.2.0的magento/product-recommendations

_2025年4月4日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)已将`recommendations-admin-ui`的CDN URL更新到`adobe.io`域。

### 6.1.0的magento/product-recommendations

_2025年3月11日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)添加了PHP 8.4支持。

### 6.0.3的magento/product-recommendations

_2024年11月6日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![修复](../assets/fix.svg)修复了[类别筛选器](filters.md#category)包含不属于当前商店评论的类别的问题。
![修复](../assets/fix.svg)修复了`magento/product-recommendations`中继包中的依赖性问题。

### 6.0.2的magento/product-recommendations

_2024年5月9日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![修复](../assets/fix.svg)修复了以下问题：在“产品推荐”单元内的简单产品上单击“**[!DNL Add to Cart]**”按钮时，购物者将被重定向到主页，而不是停留在当前页面。
![错误](../assets/bug.svg) `referenceBlock` XML文件中的`ProductRecommendations Layout`元素导致验证错误。

### 6.0.1的magento/product-recommendations

_2024年3月19日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)添加了PHP 8.3支持。

### 6.0.0个magento/product-recommendations

_2024年2月22日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg) [!DNL Catalog Sync Dashboard]现在是[[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/systems/data-transfer/data-dashboard)。 此改版后的仪表板提供[!DNL Product Recommendations]、[!DNL Live Search]和[!DNL Catalog Service]的数据流分析。
![修复](../assets/fix.svg)修复了导致[!DNL Product Recommendations]出现签出错误的问题。

+++5.0.0及更早版本

### 5.0.1的magento/product-recommendations

_2023年9月15日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)已添加新模块以支持[Saas价格索引器](../price-index/price-indexing.md)。
![新](../assets/new.svg)添加了新的数据导出模块，以支持导出更多产品类型，包括捆绑产品和礼品卡。
![修复](../assets/fix.svg)产品和价格馈送的表大小已大大减少。 表`catalog_data_exporter_products`和`catalog_data_exporter_product_prices`应该会看到大小的大幅减少。

#### 已知限制

* 如果`websiteCode`值包含下划线(_)，则错误返回该值。

### 5.0.0个magento/product-recommendations

_2023年3月20日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)已更新[!DNL Product Recommendations]以支持Adobe Commerce 2.4.6。
![新建](../assets/new.svg)这是一个主要版本版本。 [编辑](install-configure.md#update)项目的根`composer.json`文件。
![新](../assets/new.svg) [!DNL Product Recommendations]现在支持Commerce中的完整[Inventory management](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/inventory/introduction)功能(以前称为“多Source清单”或MSI)。 要启用完全支持，您必须[将](install-configure.md#update)依赖项模块`commerce-data-export`更新为版本102.2.0+。

### magento/product-recommendations的4.0.1

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![修复](../assets/fix.svg)以前，[!DNL Product Recommendations]在将显示货币转换为非默认货币时会显示错误。 现在可以正常切换货币。

### magento/product-recommendations的4.0.0

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)添加了[就绪指示器](create.md)，以帮助您可视化每个推荐类型的培训进度。
![新建](../assets/new.svg)这是一个主要版本版本。 [编辑](install-configure.md#update)项目的根`composer.json`文件。 此版本还要求您在安装和配置[!DNL Product Recommendations]时提供两个API密钥： [生产密钥和沙盒密钥](../landing/saas.md)。

#### 已知限制

* 如果`websiteCode`值包含下划线(_)，则错误返回该值。

### 3.3.7 magento/product-recommendations

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![新](../assets/new.svg)添加了PHP 8.1支持
![新建](../assets/new.svg)改进了图像大小调整，以便在参考显示模板中更一致地处理图像大小调整

### 3.3.6的magento/product-recommendations

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

通过显式列出依赖关系，![New](../assets/new.svg)优化了[!DNL Product Recommendations]中继

### 3.3.5的magento/product-recommendations

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![新](../assets/new.svg)已在[中添加](onboarding.md#b2bsupport)B2B支持[!DNL Product Recommendations]
![新](../assets/new.svg)已通过命令行将目录数据[同步到Commerce服务的新馈送添加到](https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/data-services/catalog-sync)同步

### 3.3.3的magento/product-recommendations

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![新](../assets/new.svg)已添加新的[推荐类型](type.md)：“转化”（查看购物车）、“转化”（查看购买）和“最近查看”。 这些新推荐类型在`magento/product-recommendations`模块3.2.2及更高版本中可用。
![修复](../assets/fix.svg)修复了Fastly的Web应用程序防火墙(WAF)错误地阻止Cookie的问题
![修复](../assets/fix.svg)修复了在为该特定商店视图创建推荐时，分配给非默认商店视图的产品未显示在&#x200B;_推荐产品预览_面板中的问题
![修复](../assets/fix.svg)修复了页面生成器中的某些推荐单元名称阻止推荐单元显示在店面的问题

### 3.3.2的magento/product-recommendations

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![Fix](../assets/fix.svg)修复了缺少B2B支持的依赖关系

### 3.3.1的magento/product-recommendations

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![新](../assets/new.svg)添加了B2B客户组定价支持。 当您在推荐单位上设置[价格过滤器](filters.md)时，登录的B2B客户将看到所显示产品的客户组定价集。

### 3.3.0的magento/product-recommendations

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![新](../assets/new.svg)添加了对Adobe客户端数据层的支持，以便跨Adobe Commerce功能和服务标准化行为数据收集。 请参阅[自述文件](https://github.com/adobe/commerce-events/blob/main/packages/storefront-events-collector/README.md)以了解详情。

### 3.2.6的magento/product-recommendations

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![修复](../assets/fix.svg)修复了JavaScript模式错误
![修复](../assets/fix.svg)修复了Fastly的Web应用程序防火墙(WAF)错误地阻止Cookie的问题

### 3.2.5的magento/product-recommendations

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![新](../assets/new.svg)已将Magento服务重命名为[Commerce服务](https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/integration-services/saas)，并提高了管理员的可用性

### 3.2.4的magento/product-recommendations

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![修复](../assets/fix.svg)修复了在索引产品属性时“无法检索可配置产品选项数据”错误

### 3.2.3的magento/product-recommendations

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![修复](../assets/fix.svg)修复了目录同步期间的“无法检索可配置产品选项数据”错误
![修复](../assets/fix.svg)修复了在启用“将存储代码添加到URL”配置时存储代码设置不正确的问题
![修复](../assets/fix.svg)改进了对Admin Panel配置更改的检测以确保这些更改反映在目录同步数据中

### 3.2.2的magento/product-recommendations

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![新](../assets/new.svg)添加了在创建时[预览推荐结果](create.md)的功能。 这可能需要您将模块更新到最新版本。
![新](../assets/new.svg)添加了[从管理员](https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/data-services/catalog-sync)监视和管理目录同步进程的功能。
![新](../assets/new.svg)添加了[筛选器](filters.md)以控制推荐中显示的产品。
![New](../assets/new.svg)已添加[视觉相似度](type.md#visualsim)推荐类型。

### 用于页面生成器的magento/module-page-builder-product-recommendations的1.2.1

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![新](../assets/new.svg)已添加对`magento/product-recommendations`模块的3.2.0+版本的支持

### 3.1.0的magento/product-recommendations

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![新](../assets/new.svg)已添加通过命令行[将您的目录](https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/data-services/catalog-sync)重新同步到SaaS服务的功能。
![新](../assets/new.svg)添加了对数据库表前缀的支持
![修复](../assets/fix.svg)删除了PHP 7.1支持

### 3.0.8的magento/product-recommendations

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![修复](../assets/fix.svg)修复了在配置模块之前发送用于数据收集的事件，从而导致流量无效的问题

### 3.0.6的magento/product-recommendations

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![新](../assets/new.svg) **(Beta)**&#x200B;包含对新[视觉相似度](type.md#visualsim)推荐类型的支持。

### magento/module-visual-product-recommendations的1.0.0

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![新](../assets/new.svg) **(Beta)** [视觉相似度](type.md#visualsim)。 使用&#x200B;_视觉相似度_&#x200B;推荐类型，您可以将推荐单元部署到产品详细信息页面，该页面显示与正在查看的产品视觉上类似的产品。

### 3.0.5的magento/product-recommendations

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![修复](../assets/fix.svg)修复了在目录导出期间可能发生的“无法检索产品选项数据”错误。
![修复](../assets/fix.svg) _仪表板上_ Revenue _[!DNL Product Recommendations]_&#x200B;列中的货币符号现在正确反映了配置的基本货币。

### 3.0.4的magento/product-recommendations

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![Fix](../assets/fix.svg)添加了对Adobe Commerce 2.4.0的支持

### 3.0.3的magento/product-recommendations

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![修复](../assets/fix.svg)店面模板中改进的符号实现

### 用于页面生成器的magento/module-page-builder-product-recommendations的1.0.4

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![新](../assets/new.svg)在编辑页面生成器内容类型时添加了产品推荐名称

### 3.0.2 magento/product-recommendations

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![New](../assets/new.svg)在页面生成器中选择推荐单元时在网格中添加了一个状态列
![修复](../assets/fix.svg)修复了产品和图像URL中的http/https协议不正确的问题

### 3.0.1的magento/product-recommendations

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

这是一个主版本发行版本。 [编辑](install-configure.md#update)项目的根composer.json文件。

![新建](../assets/new.svg)从备用SaaS数据空间获取[!DNL Product Recommendations]。 这允许您在其他非生产环境中使用产品环境中计算的[!DNL Product Recommendations]。 [切换SaaS数据空间](settings.md)进一步描述了此功能。

![修复](../assets/fix.svg)修复了使用uBlock Origin的购物者无法结帐的问题
![修复](../assets/fix.svg)修复了发送无关的添加到购物车事件的问题

### 用于页面生成器的magento/module-page-builder-product-recommendations的1.0.3

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![新](../assets/new.svg)页面生成器支持。 通过页面生成器集成，您可以将推荐单元准确并粒度地放置在页面生成器创作内容上的任意位置。 您还可以设置标题和推荐单位本身的样式。 有关详细信息，请转到[页面生成器](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/page-builder/add-content/recommendations)。

### 2.0.0的magento/product-recommendations

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![新](../assets/new.svg)一般可用性版本！

+++

## 文档

要了解有关[!DNL Product Recommendations]和[!DNL Product Recommendations]开发的更多信息：

* [用户指南](overview.md)
* [开发人员文档](https://experienceleague.adobe.com/zh-hans/docs/commerce/product-recommendations/developer/development-overview)
