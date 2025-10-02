---
title: '[!DNL Live Search]发行说明'
description: Adobe Commerce中 [!DNL Live Search] 的最新发行信息。
feature: Services, Search, Release Notes
exl-id: 099cf79c-968c-4381-b66d-7f6141ad2db3
source-git-commit: 6b74580a3135322f222b8cfa5c51277a34e6bb83
workflow-type: tm+mt
source-wordcount: '2589'
ht-degree: 0%

---

# [!DNL Live Search]发行说明

以下发行说明介绍了[!DNL Live Search]的最新版本。

为最新发布的版本提供支持。 提供了旧版本的发行说明以供参考。
更新包括：

![新](../assets/new.svg)新功能
![修复](../assets/fix.svg)修复和改进
![错误](../assets/bug.svg)已知问题

## 托管服务更新

这些说明描述了在未发布版本控制版本或对托管服务的改进的情况下发布的更新。

_2025年10月1日_

![新](../assets/new.svg)已添加名为`ds-logged-in`的新数据存储密钥供客户登录数据。

_2025年4月29日_

![修复](../assets/fix.svg)修复了&#x200B;**性能**&#x200B;选项卡上的&#x200B;[**导出到CSV**](./performance.md)报告未包含日期范围内指定的所有数据的问题。
![修复](../assets/fix.svg)修复了在使用搜索查询筛选器时无法保存[促销规则](./rules.md)的问题。
![修复](../assets/fix.svg)修复了[固定产品](./facets-manage.md#pinunpin-facet)未列在结果页面顶部的问题。

_2025年4月21日_

![修复](../assets/fix.svg)修复了价格范围过滤器的问题，以便不将等于上限范围的产品包含在结果中。 此更改与为Facet定义价格范围的方式保持一致。

_2025年4月3日_

![修复](../assets/fix.svg)已更新SaaS数据导出扩展以删除B2B商家的“必须将产品分配给根类别”[限制](boundaries-limits.md#b2b-and-category-permissions)。 请参阅[管理数据导出扩展](../data-export/manage-extension.md)，了解如何将SaaS数据导出扩展更新到版本103.4.0+。

_2025年2月20日_

![新](../assets/new.svg) Commerce支持多词同义词。 [了解更多](synonyms-type.md#multi-word-synonym-behavior)。 仅在2月20日这一发布日期之后才支持多词同义词。 任何现有的多词同义词都需要完全重新索引才能工作，可以通过[创建支持票证](https://experienceleague.adobe.com/zh-hans/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide)来请求此操作。

_2025年1月31日_

![新](../assets/new.svg)测试环境中无查询的目录数据有新的数据保留策略。 [了解详情](overview.md#catalog-data-retention-policy)。

_2024年9月19日_

![新](../assets/new.svg)发布了一个测试版，该版本支持三种新搜索功能：分层搜索、开头搜索和包含搜索。 [了解详情](install.md#install-the-live-search-beta)。

_2024年9月4日_

![Fix](../assets/fix.svg)将Facet[内可返回](boundaries-limits.md#facets)的最大存储段数增加到100。

_2024年8月7日_

![固定](../assets/fix.svg)将[价格分面](settings.md#price-faceting)的最大间隔值或价格范围从10,000增加到40,000,000。

_2024年2月13日_

![New](../assets/new.svg) [!DNL Live Search]现在支持为[搜索促销](rules.md)设置默认规则。

_2023年10月12日_

![新](../assets/new.svg)Commerce管理员现在可以为[!DNL Live Search]指定索引的语言。 查看[设置](settings.md)。
![修复](../assets/fix.svg)“搜索规则”选项卡已重命名为“搜索促销”。

_2023年6月13日_

![修复](../assets/fix.svg)修复了某些字符（如引号或撇号）导致排名问题的问题。 重新索引解决了这些问题。

_2023年4月25日_

![新](../assets/new.svg) [!DNL Live Search]客户现在可以利用新的[SaaS价格索引器](../price-index/price-indexing.md)。

### PLP小组件

_2025年5月22日_

![修复](../assets/fix.svg)修复了在区域设置更改为法语、德语、意大利语或西班牙语时“添加到购物车”按钮保持为英文状态的问题。
![修复](../assets/fix.svg)修复了为缺货产品显示“添加到购物车”按钮的问题。

_2024年5月31日_

![新](../assets/new.svg)发布了PLP小组件2.0.0版，其中添加了对以下功能的支持：

- 添加到购物车按钮 — 仅适用于简单产品。
- 每个产品有多个图像 — 为可配置产品选择不同颜色时，图像可能会发生更改。

_2023年10月27日_

![新建](../assets/new.svg) [!DNL Live Search] PLP小组件现在支持色板。

## [!DNL Live Search] 4.5.0

_2025年9月5日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)实时搜索现在完全遵守[Cookie限制模式](install.md#cookies)，方法是在启用限制时阻止在Cookie/本地存储中进行数据收集和存储。

## [!DNL Live Search] 4.4.1

_2025年8月11日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![修复](../assets/fix.svg)修复了沙盒环境的目录服务终结点。

## [!DNL Live Search] 4.4.0

_2025年7月14日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)已将[价格分组](./settings.md#price-faceting)限制从50增加到100。

## [!DNL Live Search] 4.3.0

_2025年3月11日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![修复](../assets/fix.svg) [!DNL Live Search]现在支持运行Adobe Commerce 2.4.8-beta2的安装使用PHP 8.4。
![修复](../assets/fix.svg)修复了搜索适配器与`psr/http-message:2.0`不兼容的问题。

## [!DNL Live Search] 4.2.3

_2025年2月13日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![修复](../assets/fix.svg)修复了订单详细信息页面缺少订单编号、日期和&#x200B;**[!UICONTROL Reorder]**&#x200B;按钮的问题。

## [!DNL Live Search] 4.2.2

_2025年1月6日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![修复](../assets/fix.svg)修复了导致Adobe Commerce版本2.4.5和更低版本上的`categoryList` GraphqL查询出错的问题。

## [!DNL Live Search] 4.2.1

_2024年7月31日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![修复](../assets/fix.svg)修复了某些脚本未在签出页面上加载的问题。
![修复](../assets/fix.svg)修复了`composer.json`文件中的依赖项版本。

## [!DNL Live Search] 4.2.0

_2024年5月31日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)更新了Live Search扩展以使用PLP小组件2.0.0版。

## [!DNL Live Search] 4.1.2

_2024年5月16日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

### 更新

![修复](../assets/fix.svg)修复了[`productSearch`](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-by-categories) GraphQL查询以根据`categoryPath`和`categoryList`正确筛选类别。

## [!DNL Live Search] 4.1.1

_2024年3月19日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

### 新增功能

![New](../assets/new.svg)添加了对波兰语的语言支持。
![New](../assets/new.svg) [!DNL Live Search]现在支持运行Adobe Commerce 2.4.4的安装使用PHP 8.3。

## [!DNL Live Search] 4.1.0

_2024年2月22日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

### 新增功能

![新](../assets/new.svg) [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/systems/data-transfer/data-dashboard)现已可用。 此改版后的仪表板提供[!DNL Product Recommendations]、[!DNL Live Search]和[!DNL Catalog Service]的数据流分析。

### 更新

![修复](../assets/fix.svg)修复了在非默认商店视图中来宾用户将产品添加到购物车时导致错误的问题。
![修复](../assets/fix.svg)修复了导致搜索弹出框始终在价格值前面显示货币符号（无论区域设置如何）的问题。
![修复](../assets/fix.svg)为已禁用的核心插件删除了不必要的类型定义，以修复安装时的兼容性问题。

## [!DNL Live Search] 4.0.0

_2023年11月13日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

### 新增功能

![New](../assets/new.svg) [!DNL Live Search]现在支持PLP小部件中的颜色色板。
![New](../assets/new.svg) [!DNL Live Search]现在显示类别名称而不是类别ID。
![New](../assets/new.svg) [!DNL Live Search]现在支持PLP小部件中的删除线价格。
![新](../assets/new.svg)引入了“隐藏筛选器”按钮以隐藏筛选器面板。


### 更新

![修复](../assets/fix.svg)对于新安装，现在默认启用[!DNL Live Search] PLP小组件。
![修复](../assets/fix.svg)已弃用搜索适配器。 今后，将仅更新搜索适配器以解决安全问题。
![修复](../assets/fix.svg)重新配置的CSS样式以更好地隔离构件类。
![修复](../assets/fix.svg)小错误修复

安装版本3.1.1或更高版本后，启用新的索引器：

- 产品价格信息源
- 范围网站数据馈送
- 范围客户组数据馈送

升级后，在将更改推送到生产环境之前，请在QA或暂存中测试更新的配置。

+++3.1.1和之前的版本

### [!DNL Live Search] 3.1.1

_2023年9月15日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

已添加![新](../assets/new.svg)新类别促销选项卡。 用户现在可以按类别添加智能排名和手动排名（固定、提升、隐藏、隐藏）
![新](../assets/new.svg)用户可以添加具有智能或手动排名的单个类别规则
![新](../assets/new.svg)用户现在可以将智能排名规则添加到子类别
![新](../assets/new.svg)删除具有智能排名的子类别时提供了详细信息
![新](../assets/new.svg)添加了删除继承排名策略规则的功能
![新](../assets/new.svg)添加了删除单个类别规则的功能
添加规则时，![新](../assets/new.svg)用户现在可以按类别名称搜索
![新](../assets/new.svg)使用类别树视图，用户现在可以查看哪个类别应用了规则。
![新建](../assets/new.svg)类别预览仅显示所选类别。
![新](../assets/new.svg) AEM CIF [Pover构件](https://github.com/adobe/aem-cif-guides-venia/pull/319)和[PLP构件](https://github.com/adobe/aem-cif-guides-venia/pull/320)组件允许AEM站点利用[!DNL Live Search]。

#### 更新

![修复](../assets/fix.svg)产品和价格馈送的表大小已大大减少。 表`catalog_data_exporter_products`和`catalog_data_exporter_product_prices`应该会看到大小的大幅减少。
![修复](../assets/fix.svg)“规则”选项卡已重命名为“搜索规则”
![修复](../assets/fix.svg)当按“趋势”进行排名时，您现在可以选择以下两项：
- 3天（默认）
- 14天
- 30天
![修复](../assets/fix.svg)“事件”（提升/固定/嵌入/隐藏）已重命名为“手动排名”
![修复](../assets/fix.svg)“排名类型”已重命名为“智能排名”
![修复](../assets/fix.svg)小错误修复

### [!DNL Live Search] 3.1.0

_2023年9月1日_

[!BADGE 支持]{type="Informative" tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

#### 更新

![修复](../assets/fix.svg)产品列表构件已更新为使用[目录服务API](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/)。

### [!DNL Live Search] 3.0.2

_2023年8月7日_

[!BADGE 支持]{type="Informative" tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

#### 新增功能

![新](../assets/new.svg)以下值已添加到`storeDetails`对象：

- &quot;允许每页所有产品&quot;
- 汇率
- “网格上每页的产品允许值”
- “网格上每页产品默认值”
- 存储语言

#### 更新

![Fix](../assets/fix.svg)目录服务模块已添加到元包以支持高级数据检索。
![修复](../assets/fix.svg)使用产品列表页面构件时，**我的帐户**&#x200B;页面导航不再消失。

商家必须升级[!DNL Live Search]扩展版本>= 3.0.2才能访问这些功能。

建议在推送到生产环境之前进行升级和测试。 在验证其测试环境结果后，请考虑在非高峰时间升级生产环境。

#### 限制

使用实时搜索产品列表页面构件会导致Google Tag Manager失败。 如果需要Google Tag Manager，请使用默认的Search Adapter 。

### [!DNL Live Search] 3.0.1

_2023年3月14日_

[!BADGE 支持]{type="Informative" tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

#### 新增功能

规则预览中的![新](../assets/new.svg)产品项卡
![新建](../assets/new.svg) [产品列表页小组件](https://experienceleague.adobe.com/zh-hans/docs/commerce/live-search/live-search-storefront/plp-styling)
![新](../assets/new.svg) [类别筛选选项](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#facets)
![新](../assets/new.svg)添加了拖放以创建Pin事件的功能
![新建](../assets/new.svg)个新Pin操作：
 — 固定到位置 — 单击一次即可固定按钮以创建固定事件
 — 固定到顶部 — 将产品放在第一个位置
 — 固定到底部 — 将产品放置在结果的底部
 — 单击一下以取消固定事件
![新](../assets/new.svg) [规则的智能排名](https://experienceleague.adobe.com/zh-hans/docs/commerce/live-search/live-search-admin/rules/rules-add)
![新](../assets/new.svg) [!DNL Live Search]现在支持Commerce中的完整[Inventory management](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/inventory/introduction)功能(以前称为多Source清单，或MSI)。 要启用完全支持，您必须[将](install.md#update)依赖项模块`commerce-data-export`更新为版本102.2.0+。

#### 更新

![修复](../assets/fix.svg)配置规则现在会自动对职位进行唯一排序
![修复](../assets/fix.svg)删除现有事件现在会更新预览
可以保存不含事件的![修复](../assets/fix.svg)规则
![修复](../assets/fix.svg)删除彩块化“选择类型”选择器
![修复](../assets/fix.svg)为未保存的规则添加了新的“编辑”状态

#### 修复

![修复](../assets/fix.svg)在保存期间存在未完成的事件时修复服务器错误
![修复](../assets/fix.svg)修复了在存在多个事件时正确删除特定事件的问题
![修复](../assets/fix.svg)修复了在添加新事件时现有规则事件未更新的问题
![修复](../assets/fix.svg)修复了第二次“编辑”点击的详细信息，[!DNL Live Search]页面需要重新加载
![修复](../assets/fix.svg)同义词：修复了当用户单击退出输入时，无法将焦点返回到字段的问题
![修复](../assets/fix.svg)其他次要错误修复和性能更新
![错误](../assets/bug.svg) — 仅在实时搜索构件中支持按“为您推荐”排名。 默认的Luma和PWA搜索功能不支持此功能。
![错误](../assets/bug.svg) — 自定义价格属性Facet在Luma中无法正确呈现，但API正确地筛选它们。

商家必须升级[!DNL Live Search]扩展版本>= 3.0.1才能访问这些功能。

建议在推送到生产环境之前进行升级和测试。 在验证其测试环境结果后，请考虑在非高峰时间升级生产环境。

### [!DNL Live Search] 2.0.5

[!BADGE 支持]{type="Informative" tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![修复](../assets/fix.svg) — 当SDK资源因网络问题而不可用时，Live Search会引发错误。 此错误已修复。

商家必须升级Live Search扩展版本>= 2.0.5才能访问这些功能。

建议在推送到生产环境之前进行升级和测试。 在验证其测试环境结果后，请考虑在非高峰时间升级生产环境。

### [!DNL Live Search] 2.0.4

[!BADGE 支持]{type="Informative" tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)实时搜索现在支持按管理员中的“显示缺货产品”设置进行筛选。 如果“显示缺货产品”设置为false，则会将`inStock = true`添加到筛选条件。
![修复](../assets/fix.svg)为了提高性能，已从“实时搜索”弹出窗口中删除“建议”块。 如果要替换该功能，数据仍会通过GraphQL传递。
![Fix](../assets/fix.svg) `categories`和`categoryPath`已替换`categoryIds`进行类别筛选。 请参阅[productSearch](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/)主题以了解详情。
![修复](../assets/fix.svg)以前，与B2B公司绑定的用户在搜索时会收到不正确的客户组代码。 Live Search现在返回正确的值。
![修复](../assets/fix.svg)以前，在搜索不存在的术语时，Live Search会返回错误。 此错误现已修复。

商家必须升级[!DNL Live Search]扩展版本>= 2.0.4才能访问这些功能。

建议用户在推送到生产环境之前进行升级和测试。 在验证其测试环境结果后，请考虑在非高峰时间升级生产环境。

### [!DNL Live Search] 2.0.3

[!BADGE 支持]{type="Informative" tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg) Live Search现在通过遵循类别权限、共享目录和特定于客户组的定价来支持B2B功能。

商家必须升级[!DNL Live Search]扩展版本>= 2.0.3才能访问这些功能。

建议用户在推送到生产环境之前进行升级和测试。 在验证其测试环境结果后，请考虑在非高峰时间升级生产环境。

### [!DNL Live Search] 2.0

[!BADGE 支持]{type="Informative" tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

现有[!DNL Live Search]安装必须升级到[!DNL Live Search] 2.0.0，才能利用以下新功能、修复和改进：

对于运行Adobe Commerce 2.4.4的安装，![New](../assets/new.svg) [!DNL Live Search]现在支持PHP 8.1。
![新](../assets/new.svg) `Magento_ElasticsearchCatalogPermissionsGraphQl`模块已添加到安装期间禁用的模块列表中。
![新](../assets/new.svg) [[!DNL storefront popover]](overview.md)中的可用行数可以从&#x200B;*管理员*中配置。
![支持](../assets/new.svg)新[&#x200B; Beta &#x200B;](https://developer.adobe.com/commerce/pwa-studio/)PWA[!DNL Live Search]。
![新建](../assets/new.svg) [!DNL Live Search]安装过程已更新，其中包含高级过程更改。
已从店面页脚中删除![修复](../assets/fix.svg) [高级搜索](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/catalog/catalog/search/search)链接。
![错误](../assets/bug.svg)以下产品属性在与PWA的Beta版一起使用时，[Commerce GraphQL API](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/)不支持： `description`、`name`、`short_description`
![错误](../assets/bug.svg) [!DNL Live Search]的PWA测试版不支持[事件处理](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/)。

### [!DNL Live Search] 1.3.1

[!BADGE 支持]{type="Informative" tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![Fix](../assets/fix.svg) [自定义价格属性](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/catalog/product-attributes/attributes-input-types)在配置为[Facet](facets-add.md)时不再返回错误。
![修复](../assets/fix.svg)修复了在没有[货币符号](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration#step-5-customize-currency-symbols-optional) (`data-currency-symbol`)可用时导致错误发生的问题。
![Fix](../assets/fix.svg) [[!DNL Storefront popover]](storefront-popover.md)现在显示[特别价格](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/catalog/products/pricing/product-price-special)（最低最终价格）（可用时）。

### [!DNL Live Search] 1.3.0

[!BADGE 支持]{type="Informative" tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![新](../assets/new.svg) [性能](performance.md)报告仪表板可为insight提供购物者使用的搜索词。
![新](../assets/new.svg) [!DNL Live Search] [Storefront事件SDK](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/)提供对公共数据层的访问，该数据层包含事件发布和订阅服务以及指标。
![修复](../assets/fix.svg) [[!DNL Storefront popover]](storefront-popover.md)具有用于控制可见性的`active`容器的新`.search-autocomplete`类。
![修复](../assets/fix.svg)在店面，[搜索词](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/catalog/catalog/search/search-terms)页脚链接已被删除，并且其缓存已为[!DNL Live Search]安装禁用。
搜索适配器的![错误](../assets/bug.svg)修补程序处理重复的产品。
![错误](../assets/bug.svg) [!DNL Live Search]支持具有多个（虚拟）[库存](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/inventory/sources/sources-manage)的[单一来源](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/inventory/stocks/stocks-manage)（物理）库存位置。 现在不支持多个清单源。

### [!DNL Live Search] 1.2.0

[!BADGE 支持]{type="Informative" tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![新](../assets/new.svg) [[!DNL Storefront popover]](storefront-popover.md)显示推荐的产品和排名最前的搜索结果的缩略图图像，购物者将查询键入搜索框。
![新](../assets/new.svg) Commerce *管理员*会话在长时间键盘不活动期间保持打开状态
![新](../assets/new.svg) [!DNL Live Search]在载入后自动启用
![修复](../assets/fix.svg)初始索引时间不到一小时
![近乎实时地修复](../assets/fix.svg)增量产品更新（安装和设置后）
在同义词编辑器中![修复](../assets/fix.svg)可排序的列
如果搜索条件包含空的排序顺序值，![修复](../assets/fix.svg) [!DNL Live Search]将不再引发错误
![修复](../assets/fix.svg)如果属性代码包含字符串“to”或“from”，则范围筛选不再中断

### [!DNL Live Search] 1.1.0

[!BADGE 支持]{type="Informative" tooltip="支持"} Adobe Commerce版本2.4.x及更高版本

![错误](../assets/bug.svg) [!DNL Live Search]服务仅支持Adobe Commerce安装的[基础货币](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration)。
![错误](../assets/bug.svg)添加Facet时，产品属性信息源在设置为`Update on Save`时未正确更新。 为避免此问题，请转到[索引管理](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/systems/tools/index-management)并将产品属性信息源设置为`Update by Schedule`。
![错误](../assets/bug.svg) [!DNL Live Search]同义词是按商店视图定义的，但当前按网站存储，并由`environmentId`和`storeViewCode`的组合标识。 因此，Adobe Commerce安装中的所有网站和存储视图会共享同义词。 最近为存储视图创建的同义词集优先。
![错误](../assets/bug.svg)如果同义词术语包含多个单词，则每个单词都被视为单独的同义词。 例如，如果将“time piece”定义为“watch”的同义词，则“time”和“piece”均被视为手表的同义词。

+++

## 文档

要了解更多信息，请执行以下操作：

- [Adobe Commerce开发人员文档](https://developer.adobe.com/commerce/docs)
- [Adobe Commerce用户指南](https://experienceleague.adobe.com/zh-hans/docs/commerce)
- Marketplace[[!DNL Live Search] 上的](https://commercemarketplace.adobe.com/magento-live-search.html)
