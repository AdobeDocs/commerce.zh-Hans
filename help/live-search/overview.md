---
title: 什么是 [!DNL Live Search]？
description: Adobe Commerce的[!DNL Live Search]提供了快速、相关且直观的搜索体验。
recommendations: noCatalog
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---

# 什么是[!DNL Live Search]？

[!DNL Live Search]是一项功能，取代了Adobe Commerce中的标准搜索功能。 [!DNL Live Search]功能随Composer一起安装，并将您的[!DNL Commerce]存储连接到[Commerce Services Connector](../landing/saas.md)。 配置后，默认搜索文本字段将替换为[!DNL Live Search]文本字段。 [!DNL Live Search]还安装产品列表页(PLP)构件，该构件在浏览搜索结果时提供强大的筛选功能。

使用[!DNL Live Search]，您可以：

- 创建有意义的搜索体验，帮助购物者和买家尽最大努力找到他们想要的。
- 利用AI支持的动态分面和响应会话内购物者行为对搜索结果进行重新排名。
- 使用基于SaaS的轻量级服务，该服务可轻松进行更新并包含在您的许可证中，从而降低了总拥有成本。
- 通过启用GraphQL API、Headless灵活性、API沙盒环境和超快SaaS来获得技术。

>[!IMPORTANT]
>
>在网站搜索方面，Adobe Commerce会为您提供各种选项。 在实施之前，请查看[边界和限制](boundaries-limits.md)信息以确保[!DNL Live Search]适合您的业务需求。

## 架构

架构的Adobe Commerce端包括托管搜索&#x200B;*管理员*、同步目录数据和运行查询服务。 安装和配置[!DNL Live Search]后，Adobe Commerce开始与SaaS服务共享搜索和目录数据。 此时，管理员用户可以设置、自定义和管理搜索[方面](facets.md)、[同义词](synonyms.md)和[促销规则](category-merch.md)。

![实时搜索数据流](assets/ls-cs-data-flow.png)

## 快速导览

由于侧重于速度、相关性和易用性，[!DNL Live Search]对购物者和商家来说都是一个游戏规则的改变者。 请观看以下视频，然后从店面快速浏览[!DNL Live Search]。

>[!VIDEO](https://video.tv.adobe.com/v/3418797?learn=on)

有关使用和配置Live Search的更深入视频，请参阅[关于 [!DNL Live Search]](https://experienceleague.adobe.com/zh-hans/docs/commerce-learn/tutorials/getting-started/capabilities/live-search-full-demonstration)的完整演示主题。

### 按键入内容搜索

当购物者在[搜索](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/catalog/catalog/search/search)框中键入查询时，[!DNL Live Search]在[弹出框](storefront-popover.md)中回复建议的产品和排名最前的搜索结果的缩略图图像。 当购物者单击建议或精选产品时，将显示[产品详细信息](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/start/storefront/storefront)页面。 弹出框页脚中的&#x200B;_查看所有_&#x200B;链接显示搜索结果页面。

对于包含两个或更多字符的查询，[!DNL Live Search]返回“键入时搜索”结果。 对于部分匹配，每个单词的最大字符数为20。 查询中的字符数无法配置。 弹出框包括`name`、`sku`和`category_ids`字段。

![店面示例 — 键入时搜索](assets/storefront-search-as-you-type.png)

### 查看所有搜索结果

要列出“键入时搜索”查询返回的所有产品，请单击弹出框页脚中的&#x200B;_查看全部_。

![店面示例 — 价格Facet](assets/storefront-view-all-search-results.png)

### 带有Facet的过滤搜索

筛选搜索使用属性值的多个维度或[方面](facets.md)作为搜索条件。 过滤器的选择由商家定义，并根据返回的产品而发生更改，最常用的方面将固定到列表顶部。

将Facet用作URL参数： `http://yourwebsite.com?color=red`，Live Search将根据这些属性值筛选结果。

### 同义词

[同义词](synonyms.md)通过包含购物者可能使用的与目录中的词不同的词来扩展查询范围并突出查询重点。 您可以微调同义词词典，让购物者保持参与和购买路径。

### 促销规则

推销[规则](rules.md)使用向搜索添加逻辑和事件的if-then语句塑造购物体验。 您可以轻松地提升或隐藏促销、季节或其他时间段内的产品。

### 搜索词支持

[!DNL Live Search]支持Commerce [搜索词重定向](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/catalog/catalog/search/search-terms)。 例如，用户可以搜索诸如“运费”之类的术语，并直接转到运费页面。

## 实时搜索组件

- [!DNL Live Search] [弹出窗口小组件](storefront-popover.md)是在包含搜索结果的搜索字段下打开的框。
- [产品列表页小组件](plp-styling.md) (PLP)提供了一个支持方面和同义词的可搜索产品列表页。 构件在Live Search 4.0.0+中安装和启用，并替换搜索适配器。
- （**已弃用**）搜索适配器是PLP小部件的前身，且随Live Search &lt; 4.0.0安装。如果您使用的是低于4.0.0的Live Search版本，Commerce建议您进行升级，以便享受PLP构件功能和未来改进带来的好处。 今后，将仅更新搜索适配器以解决安全问题。

## [!DNL Live Search]工作区

[!DNL Live Search] [工作区](workspace.md)是管理员中配置[!DNL Live Search]功能（如同义词、Facet和类别促销）的区域。

## 活动

[!DNL Live Search]使用[事件](events.md)计算[智能促销](category-merch.md)和[性能](performance.md)仪表板。 事件随默认实施一起提供。 Headless店面的事件应该手动启用。

## 目录数据保留策略

如果您连续90天没有在测试环境中提交目录数据的搜索查询，则目录数据将设置为休眠模式，并且任何搜索查询都不会返回任何数据。 此策略不会影响生产环境中的目录数据。

要在测试环境中重新激活目录数据，请[提交标题为“重新激活[!DNL Live Search]”的支持请求](https://experienceleague.adobe.com/zh-hans/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#experience-league-start-page)并包含环境ID。 测试环境中的目录数据应在几小时内恢复。
