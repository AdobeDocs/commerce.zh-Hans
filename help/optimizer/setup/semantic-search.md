---
title: 语义搜索
description: 在 [!DNL Adobe Commerce Optimizer] 的“设置”中启用AI语义搜索。 无需属性设置或店面变更。
role: Admin, User
recommendations: noCatalog
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和 [!DNL Adobe Commerce Optimizer] 项目（Adobe管理的SaaS基础架构）。"
source-git-commit: 015f88e540fe5bf7acc4469d7c91b4f606709809
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 0%

---

# 语义搜索

语义搜索使用人工智能来理解购物者的含义，而不仅仅是他们键入的准确单词。 即使您的目录没有使用相关短语，诸如“海滩婚礼的礼服”或“整天穿着舒适的鞋子”之类的查询也可以返回相关产品。

[!DNL Adobe Commerce Optimizer]将关键字匹配和语义匹配合并到一个搜索体验中。 您不会在店面中管理单独的关键字和语义模式。 在“管理员”中，转到[设置](../settings.md#advanced-search)工作区以管理语义搜索并可以选择调整&#x200B;**[!UICONTROL Advanced search]**&#x200B;选项卡上的高级控件。

## 优点

- **更少的空搜索页面** — 当购物者的措辞与目录文本不完全匹配时，购物者可以找到产品。
- **更好的意图匹配** — 自然、描述性查询返回有用的结果。
- **少同义词维护** — 常用单词变体（例如，沙发和沙发）通常无需手动同义词列表即可处理。
- **没有店面或开发人员工作** — 默认情况下启用语义搜索，不需要主题代码、下拉列表或API更改。

## 工作原理

启用语义搜索后，[!DNL Adobe Commerce Optimizer]使用系统选择的预定义目录属性（如产品名称和描述）来解释查询含义以及传统关键词搜索。 您不会在“管理员”中选择或区分属性的优先级。

例如：

- 搜寻“皮沙发”可以找到标示为“皮沙发”的产品。
- “春天连衣裙”可以浮出水面，即使产品名称中没有“春天”。
- “跑步鞋”可与越野或登山鞋类产品相媲美。

## 启用语义搜索时会发生什么情况

语义搜索可与您现有的[!DNL Adobe Commerce Optimizer]搜索配置配合使用。 您不替换关键词搜索或重新配置店面。

当语义搜索处于活动状态时：

- 您现有的[促销规则](../merchandising/rules/overview.md)、[同义词](../merchandising/synonyms/overview.md)、[方面](../merchandising/facets/overview.md)、提升和筛选器将继续应用。
- 语义搜索增加了人工智能支持的对购物者意图的理解，以在关键词匹配的同时提高结果相关性。
- 预定义的目录属性会自动编入索引。 您不选择属性或发布单独的配置。

## 在管理员中管理语义搜索

对于符合条件的英文目录，语义搜索默认为&#x200B;**启用**。 转到&#x200B;**[!UICONTROL Settings]** > **[!UICONTROL Advanced search]**&#x200B;以确认设置或进行更改：

1. 在“管理员”中，转到&#x200B;**[!UICONTROL Settings]**。
1. 在&#x200B;**[!UICONTROL Advanced search]**&#x200B;选项卡上，查看&#x200B;**[!UICONTROL Enable semantic search]**。

   启用后，搜索将根据含义和上下文匹配产品，这可以生成更相关的结果，减少空搜索页面，并提高转化。

1. 如果更改切换或优化控件，请单击&#x200B;**[!UICONTROL Save]**。

   索引完成后，搜索结果会更新。 对于中等大小的目录，索引可能最多需要半小时。 对于包含数百万种产品的大型目录，这可能需要几个小时。

>[!NOTE]
>
> 语义搜索仅适用于&#x200B;**英语**&#x200B;目录。 如果您将&#x200B;**[!UICONTROL Language]**&#x200B;更改为非英语目录，则会自动禁用&#x200B;**[!UICONTROL Enable semantic search]**。

保存后，您无需发布单独的配置或更改店面设置。

## 启用后验证

在语义搜索处于活动状态并完成索引编制后，Adobe建议验证搜索性能。 使用[搜索性能](../manage-results/search-performance.md)页面可查看对您的业务重要的量度和测试查询。

1. 查看&#x200B;**唯一搜索**&#x200B;报表中排名最前的搜索词。
1. 从店面上的&#x200B;**零结果**&#x200B;报告中测试历史零结果查询。
1. 比较启用前后相同查询的搜索结果。
1. 监控搜索转化和参与量度，包括点进率、转化率和零结果率。

## 可选调整

在&#x200B;**[!UICONTROL Advanced search]**&#x200B;选项卡上，您可以调整在启用语义搜索后搜索的行为方式：

- **[!UICONTROL Semantic boost]** — 增加或减少基于含义的强匹配对排名的影响。 例如，假设通过语义搜索检索到的产品匹配项显示在结果末尾。 加上提振，结果中提速幅度会更高。
- **[!UICONTROL Similarity threshold]** — 设置匹配项在产品出现之前必须接近的程度。 值越小，显示的结果越多；值越高，显示的匹配越少，越紧密。
- **[!UICONTROL Fuzzy search]**&#x200B;和&#x200B;**[!UICONTROL Fuzzy search similarity threshold]** — 当查询包含较小的拼写差异时，帮助购物者查找产品。

有关控制说明和分步指南，请参阅[高级搜索](../settings.md#advanced-search)。

## 最佳实践

- 使用清晰的、描述性的产品名称和描述（最好是50-100字），以便关键词和语义匹配都具有强大的目录文本可供使用。
- 从默认&#x200B;**[!UICONTROL Enable semantic search]**&#x200B;设置开始，然后仅在结果范围太广或太窄时才调整&#x200B;**[!UICONTROL Semantic boost]**&#x200B;或&#x200B;**[!UICONTROL Similarity threshold]**。
- 保留特定品牌或技术含量较高的[同义词](../merchandising/synonyms/overview.md)，其中语义搜索可能不包含专用术语。

## 故障排除

| 问题 | 要做什么 |
| --- | --- |
| 保存后店面没有变化 | 等待索引完成。 大型目录可能需要更长的时间。 |
| 结果过于宽泛 | 在&#x200B;**[!UICONTROL Advanced search]**&#x200B;选项卡上提高&#x200B;**[!UICONTROL Similarity threshold]**&#x200B;或降低&#x200B;**[!UICONTROL Semantic boost]**。 |
| 结果感觉太窄 | 降低&#x200B;**[!UICONTROL Similarity threshold]**&#x200B;或提高&#x200B;**[!UICONTROL Semantic boost]**。 |
| 语义搜索不可用 | 确认&#x200B;**[!UICONTROL Language]**&#x200B;设置为&#x200B;**英语**。 |

## 限制 {#semantic-search-limitations}

- **目录语言：**&#x200B;语义搜索仅可用于&#x200B;**英语**&#x200B;语言目录。

## 有关此主题的更多帮助

- [高级搜索](../settings.md#advanced-search)
- [同义词](../merchandising/synonyms/overview.md)
- [搜索性能](../manage-results/search-performance.md)
