---
title: 边界和限制
description: 了解 [!DNL Live Search] 的界限和限制，以确保它满足您的业务需求。
role: Admin, Developer
exl-id: 28b8d98f-0784-4c4d-b382-81c01838e0de
source-git-commit: ff5c717dbdd638e114bccc3f6dec26f4be269194
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 0%

---

# 边界和限制

在网站搜索方面，Adobe Commerce会为您提供各种选项。 查看以下边界和限制以确保[!DNL Live Search]和[!DNL Catalog Service]满足您的业务需求。 如果您需要高级搜索功能，例如内容搜索、自带算法(BYOA)或基于属性的促销，请考虑使用第三方搜索解决方案。

## 常规

- 安装[!DNL Live Search]后，[高级搜索](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search)模块被禁用，店面页脚中的高级搜索链接被删除。
- [层定价](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/pricing/product-price-tier)在[!DNL Live Search]字段和产品列表页小部件中不受支持。
- 产品价格包含增值税(VAT)，但[!DNL Live Search]不能将增值税显示为单独的值。
- 不支持内容搜索(CMS页面和块)。
- 可分页的结果数量上限为10,000。 为了确保购物者在类别或搜索结果中包含大量产品时不必使用深度分页，请提供有意义的方法来过滤产品。
- 每个属性（包括描述和自定义属性）硬限制为1MB。
- 搜索适配器不支持使用自定义源模型创建并用作彩块化的产品属性。 若要支持此功能，您必须使用[产品列表页小组件](plp-styling.md)。
- 不支持自定义产品类型。
- 不支持用`"is_user_defined": false`编程创建的自定义属性。
- 您可以使用“开头为”或“包含”条件筛选结果，但存在一些限制，如[此处](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#limitations)所述。
- 您只能跟踪去年内的绩效指标。
- 如果搜索查询包含多个单词，则单词之间的空格会导致将它们视为单独的搜索词。 如果要考虑多词搜索查询，请使用[同义词](./synonyms.md)。

## 索引

- [!DNL Live Search] [索引](indexing.md)每个商店视图最多包含450个产品属性。 其分布情况如下：
   - 50个可排序的属性
   - 200个可过滤属性
   - 200个可搜索属性
- [!DNL Live Search]仅对Adobe Commerce数据库中的产品编制索引。
- CMS页面未编制索引。
- 默认情况下，SKU、名称和类别属性可搜索，并且无法从搜索中排除。 如果类别中没有预期的产品，请确保从这些类别中取消分配这些产品。

## Facet

- 最多可以将100个属性配置为可编制索引的200个可筛选属性中的Facet。
- 在一个Facet中，最多可返回100个分段。 如果您需要返回100个以上的分段，请[创建一个支持票证](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide)，以便Adobe分析性能影响并确定为您的环境提高此限制是否可行。
- 动态Facet会导致大型索引和高序度索引的性能问题。 如果您已创建动态Facet，并且发现任何性能下降或页面未加载但存在超时错误，请尝试将您的Facet更改为Pinded以确定这是否解决了您的性能问题。
- Stock状态(`quantity_and_stock_status`)不支持作为Facet。 您可以使用`inStock: 'true'`筛选缺货产品。 当[!DNL Commerce]管理员中的“Display out of stock products”设置为“True”时，`LiveSearchAdapter`模块即开即用支持此功能。
- 不支持将日期类型属性作为Facet。
- 将属性添加为Facet后，对该属性元数据所做的任何更改都不会反映在Facet中。

## 查询

- [!DNL Live Search]对查询使用唯一的[GraphQL端点](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/)以支持动态彩块化和按类型搜索等功能。 尽管与[GraphQL API](https://developer.adobe.com/commerce/webapi/graphql/)类似，但存在一些差异，并且某些字段可能不完全兼容。
- 搜索查询中可返回的最大结果数为10,000。
- 每页结果的最大数量为500。
- 无法使用日期类型属性筛选结果。

## 搜索促销

- 每个存储视图的最大搜索推销[规则](rules.md)数为50。
- 每个规则的最大条件数为10。
- 每个规则的最大事件数为25。
- 当选择默认排序顺序“排序依据：最相关”时，规则和手动排名产品将应用于搜索结果。 如果购物者将排序顺序更改为诸如按名称或价格排序，则规则和手动排名不再有效。
- 为了避免分页响应产生不可预测的结果，固定产品的数量不应超过请求的页面大小。

## 同义词

- [!DNL Live Search]在每个存储视图中最多可管理200个[同义词](synonyms.md)。

## 类别促销

- 您可以为每个商店视图为每个类别创建一个规则。
- 每个规则的最大条件数为10。
- 每个规则的最大事件数为25。
- 当在店面中打开特定类别并且存在该类别的规则时，将应用规则。 对于类别促销规则，默认排序顺序为“排序依据：位置”。 如果购物者更改排序顺序，则所有隐藏、固定和隐藏的产品将不再排序。

## B2B和类别权限

- 如果产品未添加到默认共享目录，则不会显示产品。
- 使用[类别权限](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/categories/category-permissions)限制客户组：
   - 必须将产品分配给根类别。 (**注意：**&#x200B;您可以通过将SaaS Data Export扩展更新到103.4.0+版来移除此限制。 请参阅[管理数据导出扩展](../data-export/manage-extension.md)。
   - 必须向“未登录”客户组提供“允许”浏览权限。
   - 要将产品限制为“未登录”客户组，请转到每个类别并为每个[客户组](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/shared-catalogs/catalog-shared-manage)设置权限。
- 目前不支持在PWA Studio中使用PLP小组件对B2B提供开箱即用支持。 但是，您可以[使用API](install.md#pwa-support)来实施此功能。
- [!DNL Live Search]中的类别Facet可能显示无法显示给特定[客户组](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/shared-catalogs/catalog-shared-manage)的类别。
- [!DNL Live Search]最多可支持1,000个客户组。

## [!DNL Storefront popover]

- [[!DNL popover]](storefront-popover.md)仅适用于使用&#x200B;*Luma*&#x200B;主题或基于&#x200B;*Luma*&#x200B;的自定义主题的商店。 搜索结果页面上的痕迹导航将没有&#x200B;*Luma*&#x200B;样式。
- [!DNL popover]不支持&#x200B;*Blank*&#x200B;主题。
- 快速订购单不支持[!DNL popover]。
- 不支持愿望清单和产品比较。
- 不支持秘鲁索尔(PEN)的货币符号。

## 故障排除

有关对[!DNL Live Search]中的一些常见问题进行故障排除的帮助，请参阅以下知识库文章：

- [[!DNL Live Search] 目录未同步](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-catalog-data-sync)
- [[!DNL Live Search] 仪表板和搜索结果排名不正确](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-dashboard-ranking-incorrect)
- [[!DNL Live Search] 显示缺货产品，而不管管理员中的库存状态设置如何](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-displays-out-of-stock-products)
- [[!DNL Live Search] 方面未按字母顺序排序](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-facets-not-sorted)

如果您需要其他帮助，请联系[支持](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide)。
