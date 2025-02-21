---
title: 索引
description: 了解 [!DNL Live Search] 如何索引产品属性属性。
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 0%

---

# 索引

[!DNL Live Search]索引过程读取产品属性的目录并构建索引，以便快速搜索、过滤和展示产品。

产品属性属性（元数据）确定：

* 如何在目录中使用属性
* 它在商店中的外观和行为
* 数据传输操作中包含的数据

属性元数据的范围是`website/store/store view`。

[!DNL Live Search] API允许客户端按Adobe Commerce管理员中将[storefront属性](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/product-attributes) `Use in Search`设置为`Yes`的任何产品属性进行排序。 启用后，可以为属性设置`Search Weight`。

[!DNL Live Search]不为已删除的产品或设置为`Not Visible Individually`的产品编制索引。

>[!NOTE]
>
> 拥有[!DNL Live Search]的Commerce客户可以使用[SaaS价格索引器](../price-index/price-indexing.md)利用其网站上更快的价格更改更新和同步时间。

## 索引管道

客户端从店面调用搜索服务以检索（可筛选、可排序）索引元数据。 搜索服务只能调用可搜索的产品属性，该属性的&#x200B;*用于分层导航*&#x200B;属性设置为`Filterable (with results)`，*用于产品列表排序*&#x200B;设置为`Yes`。

要构造动态查询，搜索服务需要知道哪些属性是可搜索的，以及它们的[权重](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search-results)。 [!DNL Live Search]遵循Adobe Commerce搜索权重（1-10，其中10是最高优先级）。 可以在架构中找到同步并与目录服务共享的数据列表，架构定义于：

`vendor/magento/module-catalog-data-exporter/etc/et_schema.xml`

![[!DNL Live Search]索引客户端搜索关系图](assets/indexing-pipeline.svg)

1. 检查[!DNL Live Search]权利的商人。
1. 获取对属性元数据进行了更改的存储视图。
1. 存储索引属性。
1. 重新索引搜索索引。

### 完整索引

如果配置了[!DNL Live Search]并在载入期间同步，则生成初始索引最多可能需要60分钟。 大型目录可能需要更长的时间来编制索引。 该进程在`cron`提交信息源并结束运行后开始。

以下事件会触发完全同步和索引生成：

* 正在载入[目录数据同步](install.md#synchronize-catalog-data)
* 属性元数据的更改

例如，将`color`属性的`Use in Search`属性从`No`更改为`Yes`将属性元数据更改为`searchable=true`，并触发完全同步和重新索引。 更改时，以下属性元数据会触发完全同步和重新索引：

* `filterableInSearch`
* `searchable`
* `sortable`
* `visibleInSearch`

### 流式产品更新

在[上线](install.md#synchronize-catalog-data)期间生成初始索引后，将持续同步并重新编制以下增量产品更新的索引：

* 添加到目录的新产品
* 产品属性值的更改

例如，将新样本值添加到`color`属性会作为流式产品更新处理。

流式更新工作流：

1. 更新的产品已从Adobe Commerce实例同步到目录服务。
1. 索引服务不断从目录服务中查找产品更新。 更新的产品在到达目录服务时会编制索引。
1. 产品更新可能最多需要15分钟才能在[!DNL Live Search]中可用。

#### 影响产品可见性的更新

当您更新[!DNL Live Search]管理员配置设置、Adobe Commerce管理员配置设置或更新目录数据时，这些更改可能会延迟出现在店面上。

下表描述了各种更改以及这些更改出现在店面之前的大致等待时间。

| 更新 | 延迟到店面可见 |
|---|---|
| [!DNL Live Search]管理员对Facet、价格设置、搜索或类别促销规则进行了更改。 | 15-20分钟。 |
| [!DNL Live Search]需要重新索引的管理更改：语言设置或同义词。 | 在索引完成后，最多可等待15分钟。 |
| 需要完全重新索引的Adobe Commerce管理更改：可搜索、可排序或可过滤的属性元数据 | 在索引完成后，最多可等待15分钟。 |
| 目录数据中不需要索引的增量更改：产品库存、价格、名称等。 | 在Elastic Search索引使用最新数据更新后最多15分钟。 |

## 客户端搜索

[!DNL Live Search] API允许客户端通过将[storefront属性](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/product-attributes)、*产品列表*&#x200B;中用于排序的`Yes`来按任何可排序的产品属性进行排序。 根据主题，此设置会导致属性作为选项包含在目录页面上的[排序方式](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/navigation/navigation)分页控件中。 [!DNL Live Search]最多可以为200个产品属性编制索引，其中[storefront属性](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/product-attributes)可搜索和过滤。

索引元数据存储在索引管道中，可供搜索服务访问。

![[!DNL Live Search]索引元数据API图](assets/index-metadata-api.svg)

### 可排序的属性工作流

1. 客户端调用搜索服务。
1. 搜索服务调用搜索管理员服务。
1. 搜索服务调用索引管道。

## 已为所有产品编制索引

此列表中字段的顺序反映了导出产品数据中的典型列顺序。

* `environment_id`
* `website_code`
* `store_code`
* `store_view_code`
* `product_id`
* `sku`
* `name`
* `type`
* `displayable`
* `deleted`
* `url`
* `currency`
* `meta_description`
* `meta_keyword`
* `meta_title`
* `description`
* `short_description`
* `weight`
* `image`
* `small_image`
* `thumbnail_image`
* `prices`
* `in_stock`
* `low_stock`

以下字段已针对所有可配置产品编制索引：

* `childrenSkus`
