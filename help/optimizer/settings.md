---
title: 设置
description: 配置 [!DNL Adobe Commerce Optimizer]的设置。
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和 [!DNL Adobe Commerce Optimizer] 项目（Adobe管理的SaaS基础架构）。"
exl-id: 6ac223de-8e03-4842-8b67-92ce321d323d
TQID: https://experienceleague.adobe.com/9-BMXoWad0bbvsnwgHQrs19ZC9ngGrVE9J7PszcX4Zc
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 015f88e540fe5bf7acc4469d7c91b4f606709809
workflow-type: tm+mt
source-wordcount: 867
ht-degree: 0%

---

# 设置

使用&#x200B;*设置*&#x200B;工作区为店面配置搜索和产品发现。 可以使用以下选项卡：

- **价格Facet** — 配置用作搜索过滤器的价格范围组和间隔。
- **语言** — 设置用于索引和搜索的目录语言。
- **高级搜索** — 启用语义搜索和模糊搜索，并调整语义提升和相似性阈值。

>[!BEGINTABS]

>[!TAB 价格Facet]

## 价格Facet {#price-facets}

您可以指定价格范围组的数量以及价格值在它们之间的分配方式。 每个价格范围与上一组价目表各一重叠。 例如，如果您使用间隔为20的5个组，则会获得价格范围，例如0-20、20-40、40-60、60-80和>80。 如果目录中没有足够的产品来填满所有定义的范围，则会相应地调整可用组的显示。 例如：0-20、60-80、>80。

**配置价格彩块化：**

1. 在&#x200B;**设置**&#x200B;工作区上，选择&#x200B;**[!UICONTROL Facets]**。
1. 在&#x200B;**价格Facet**&#x200B;部分中，执行以下操作：
   - 输入可用的&#x200B;**[!UICONTROL Number of selections]**&#x200B;或价格分组。 最多可以定义100个价格分组。
   - 输入每个组的&#x200B;**[!UICONTROL Interval value]**&#x200B;或价格范围。 最大值为40,000,000。
1. 单击&#x200B;**[!UICONTROL Save]**。

   更新后的设置大约需要15分钟才能在店面中提供。

### 字段描述

| 字段 | 描述 |
| --- | --- |
| 选择数量 | 指定可在店面中用作搜索过滤器的价格范围分组的数量。 默认值：8，最大值：100 |
| 间隔值 | 指定每个组的价格范围间隔。 例如，间隔值为20的五种选择，产量分组为0-20、20-40、40-60、60-80和>80。 默认值：5，最大值：40,000,000 |

>[!TAB 语言]

## 语言 {#language}

Language设置告知[!DNL Adobe Commerce Optimizer]在读取目录和写入索引时应该使用哪种语言。

语言有不同的语法规则集：例如单词的分隔、动词句子和单词形式。
语言设置可确保将正确的规则集应用于索引机制。

将语言设置设置为目录的主要语言。 在更改索引的语言时，根据目录的大小和复杂性，可能需要5到60分钟的时间才能将更改显示在店面上。

| 语言 | 代码 |
|----|----|
| 阿拉伯语 | ar |
| 亚美尼亚语 | hy |
| 巴斯克语 | 欧盟 |
| 孟加拉语 | bn |
| 巴西语 | pt-br |
| 保加利亚语 | bg |
| 加泰罗尼亚语 | ca |
| 中文（简体） | zh-cn |
| 繁体中文 | zh-tw |
| 捷克语 | cs |
| 丹麦语 | da |
| 荷兰语 | nl |
| 英语 | en |
| 爱沙尼亚语 | et |
| 芬兰语 | fi |
| 法语 | fr |
| 加利西亚语 | gl |
| 德语 | de |
| 希腊语 | el |
| 印地语 | 您好 |
| 匈牙利语 | 胡 |
| 印尼语 | id |
| 爱尔兰语 | ga |
| 意大利语 | it |
| 日语（片假名） | ja |
| 朝鲜语 | ko |
| 拉脱维亚语 | lv |
| 立陶宛语 | lt |
| 挪威语 | 否 |
| 波斯语 | fa |
| 葡萄牙语 | pt |
| 罗马尼亚语 | ro |
| 俄语 | ru |
| 索拉尼 | ku |
| 西班牙语 | es |
| 瑞典语 | sv |
| 土耳其语 | tr |
| 泰语 | th |

>[!TAB 高级搜索]

## 高级搜索 {#advanced-search}

使用&#x200B;**[!UICONTROL Advanced search]**&#x200B;选项卡在一个位置管理搜索。 [!DNL Adobe Commerce Optimizer]在店面中提供统一的搜索体验；您没有为购物者单独配置关键词搜索和语义搜索。 **[!UICONTROL Enable semantic search]**&#x200B;默认为&#x200B;**为符合条件的英语目录启用**。 语义搜索可与您的现有配置配合使用；[促销规则](./merchandising/rules/overview.md)、[同义词](./merchandising/synonyms/overview.md)、[方面](./merchandising/facets/overview.md)、提升和筛选器将继续应用。 系统自动使用预定义的目录属性 — 您不会在“管理员”中选择或排列属性的优先级。 无需更改店面或开发人员。

![高级搜索设置](./assets/advanced-search.png)

**要管理语义搜索：**

1. 在&#x200B;**设置**&#x200B;工作区上，选择&#x200B;**[!UICONTROL Advanced search]**&#x200B;选项卡。
1. 在&#x200B;**[!UICONTROL Enable semantic search]**&#x200B;下，确认已启用语义搜索，如果不想进行语义匹配，则禁用语义搜索。
1. 如果更改切换或优化控件，请单击&#x200B;**[!UICONTROL Save]**。

   索引完成后，搜索结果会更新。 对于中等大小的目录，索引可能最多需要半小时。 对于包含数百万种产品的大型目录，这可能需要几个小时。

### 可选调整

启用语义搜索后，可以在同一选项卡上调整以下内容：

- **[!UICONTROL Semantic boost]** — 应用提升以在排名中优先考虑语义相关的结果。 当语义匹配在结果集中权重较大时提高值；当结果感觉过于宽泛时降低值。
- **[!UICONTROL Similarity threshold]** — 设置语义匹配的最低相似度分数（百分比）。 较低的值会返回更多结果（更高的召回率），但可能包括较弱的匹配。 值越大，返回的匹配就越少，就越匹配（精度越高）。

  >[!NOTE]
  >
  > 仅&#x200B;**英文**&#x200B;目录支持语义搜索。 在&#x200B;**[语言](#language)**&#x200B;选项卡上选择其他语言将禁用&#x200B;**[!UICONTROL Enable semantic search]**。

- **[!UICONTROL Fuzzy search]** — 启用&#x200B;**以查找搜索查询的近匹配项**，这有助于更正拼写错误和次要变体。
- **[!UICONTROL Fuzzy search similarity threshold]** — 设置显示模糊匹配所需的最小相似度（百分比）。 较低的阈值会返回比较接近的匹配项；如果模糊结果过于宽泛，则提高阈值。

有关好处、验证指南、最佳实践、故障排除和限制，请参阅[语义搜索](setup/semantic-search.md)。

### 字段描述

| 控件 | 描述 |
| --- | --- |
| 启用语义搜索 | 启用后，搜索在关键词匹配旁使用含义和上下文。 自动使用预定义的目录属性；管理员中不需要设置属性。 默认为[!DNL Adobe Commerce Optimizer]客户启用。 |
| 语义提升 | 应用了Boost以优先处理排名中语义相关的结果。 |
| 相似度阈值 | 语义匹配的最小相似度分数（百分比）。 值越低越有利于召回；值越高越有利于准确性。 |
| 模糊搜索 | 当&#x200B;**在**&#x200B;时，搜索将查找查询的近匹配项（例如，次要变体）。 |
| 模糊搜索相似度阈值 | 最小相似性（百分比）模糊匹配必须满足才能显示在结果中。 |

>[!ENDTABS]
