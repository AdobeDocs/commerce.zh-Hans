---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%
---
语义搜索使用人工智能来理解购物者的含义，而不仅仅是他们键入的准确单词。 即使您的目录没有使用相关短语，诸如“海滩婚礼的礼服”或“整天穿着舒适的鞋子”之类的查询也可以返回相关产品。

产品发现系统将关键字匹配和语义匹配结合在一个搜索体验中。 您不会在店面中管理单独的关键字和语义模式。

## 配置语义搜索

对于符合条件的英文目录，语义搜索默认为&#x200B;**启用**。 您可以在[设置](../settings.md#advanced-search)工作区的&#x200B;**[!UICONTROL Advanced search]**&#x200B;选项卡中对其进行管理，在该选项卡中，您可以确认或更改设置，还可以选择性地调整语义提升、相似度阈值和模糊搜索。 有关如何打开工作区，请参阅[设置](../settings.md#access-the-settings-workspace)。

保存后，您无需发布单独的配置或更改店面设置。

## 优点

- **更少的空搜索页面** — 购物者在其措辞与目录文本不完全匹配时查找产品。
- **更好的意图匹配** — 自然的描述性查询返回有用的结果。
- **少同义词维护** — 常用词变化（例如，沙发和沙发）通常无需手动同义词列表即可处理。
- **没有店面或开发人员工作** — 默认情况下启用语义搜索，不需要主题代码、下拉列表或API更改。

## 工作原理

如果启用了语义搜索，则系统使用预定义的目录属性（如产品名称和描述）来解释与传统关键词搜索相同的查询含义。 您不会在“设置”中选择或排列属性的优先级。

例如：

- 搜寻“皮沙发”可以找到标示为“皮沙发”的产品。
- “春天连衣裙”可以浮出水面，即使产品名称中没有“春天”。
- “跑步鞋”可与越野或登山鞋类产品相媲美。

## 启用语义搜索时会发生什么情况

语义搜索可与现有搜索配置配合使用。 您不替换关键词搜索或重新配置店面。

当语义搜索处于活动状态时：

- 您现有的[促销规则](../merchandising/rules/overview.md)、[同义词](../merchandising/synonyms/overview.md)、[方面](../merchandising/facets/overview.md)、提升和筛选器将继续应用。
- 语义搜索增加了人工智能支持的对购物者意图的理解，以在关键词匹配的同时提高结果相关性。
- 预定义的目录属性会自动编入索引。 您不选择属性或发布单独的配置。

## 启用后验证

在语义搜索处于活动状态并完成索引编制后，Adobe建议验证搜索性能。 使用[搜索性能](../manage-results/search-performance.md)页面可查看对您的业务重要的量度和测试查询。

1. 查看&#x200B;**唯一搜索**&#x200B;报表中排名最前的搜索词。
1. 从店面上的&#x200B;**零结果**&#x200B;报告中测试历史零结果查询。
1. 比较启用前后相同查询的搜索结果。
1. 监控搜索转化和参与量度，包括点进率、转化率和零结果率。

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
