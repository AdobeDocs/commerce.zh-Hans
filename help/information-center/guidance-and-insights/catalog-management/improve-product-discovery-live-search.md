---
title: 利用Adobe Commerce Live Search改进产品发现
description: 了解如何使用搜索性能洞察和语义搜索来帮助购物者查找相关产品。
audience: Merchandisers, commerce administrators, and store owners
autotag-review: '2026-10-21T12:57:39.807Z'
TQID: 'https://experienceleague.adobe.com/vUbbKdcd7RFb3YUNNjlW4u7AgtiXJKeZeRs9uJwxYyY'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 76cfaac4-e563-56dd-8938-708bf8b84956
    internal-label: Attributes
  - id: cdfd3bc1-dc23-5cf0-b965-d3c0c55cde67
    internal-label: Best Practices
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
    internal-label: Catalog management
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: 125c1f49-aefd-5f34-a252-288937f95f6b
    internal-label: Marketing Tools
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
    internal-label: Insights
source-git-commit: f54c816fd23786ec519d5c890bc2664c3dcf8c6f
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 0%
---

# 利用Adobe Commerce Live Search改进产品发现

<table style="table-layout:auto">
<tr style="border: 0;">
   <td valign="middle" style="vertical-align: middle;"><img alt="桑德拉·冈萨雷斯·曼加纳的肖像" src="../../assets/guidance-and-insights/live-search-author-avatar-sgonzalezmangana.png" width="96"><br><strong>Sandra Gonzalez Mangana</strong><br><em>高级产品经理</em></td>
</tr>
</table>

*通过搜索性能分析和语义搜索，帮助购物者找到他们需要的产品。*

在目录中拥有正确的产品只是购物体验的一部分。 购物者还需要能够使用他们自然使用的词语、短语和问题找到这些产品。

Adobe Commerce Live Search提供搜索性能见解，可帮助您发现发现问题并改进体验。 利用这些见解来调查消费者在哪里遇到困难，而不仅仅是搜索结果是否返回。

## 在搜索性能中查找信号

在实时搜索性能工作区中，查看量度，例如唯一搜索、零结果搜索、热门结果、点进率、转化率和平均点击位置。 使用它们确定趋势并决定哪些查询或产品需要关注。 [性能](https://experienceleague.adobe.com/zh-hans/docs/commerce/live-search/live-search-admin/performance)

![实时搜索性能工作区显示独特搜索、平均点击位置、点进率、转化率和零结果率，并带有用于独特搜索、零结果和常用结果的选项卡](../../assets/guidance-and-insights/live-search-performance-dashboard.png){width="800" zoomable="yes"}

*实时搜索性能工作区显示要审查的量度。 显示的值是示例数据。*

考虑以下信号：

- **零结果搜索：**&#x200B;没有结果的查询可能指向您的目录、产品信息或搜索设置中的空白。 目标是将零结果搜索率保持在5%以下。 高于此阈值的速率是一个值得研究的信号。
- **低点进或弱点进位置：**&#x200B;购物者可能看到与其需求不匹配的结果，或者相关产品可能不够突出。 为确保参与，请至少瞄准50%的搜索以导致产品点击。
- **来自搜索的低转化率：**&#x200B;查看搜索是否正在帮助购物者从查询转移到购买。 目标转化率高于3%。

将它们视为基准和诊断信号，而不是普遍的“通过还是失败”。 性能因行业、目录复杂性、客户行为以及每个量度的衡量方式而异。 为您的存储建立一个基准，并比较一段时间内的性能。 结果可能因您的目录、购物者以及您衡量结果的方式而异。

## 匹配购物者意图，而不仅仅是精确的单词

购物者并不总是使用目录中的术语描述产品。 比如，寻找“适合整天站立的舒适鞋子”的人可能会对所谓的“缓冲式步行运动鞋”感兴趣。

语义搜索使用含义和上下文以及关键词匹配，帮助将自然语言查询连接到相关产品，即使查询与目录文字不完全匹配。 实时搜索将关键词和语义匹配合并到一个搜索体验中。 [语义搜索](https://experienceleague.adobe.com/zh-hans/docs/commerce/live-search/live-search-admin/semantic-search)

语义匹配有助于探索性搜索，但相关性仍然取决于目录中可用的产品和信息。 对于涉及精确模型、规范或兼容性要求的搜索，检查结果是否保持精确。

## 检查部署的语义搜索

具体取决于您使用的Adobe Commerce产品：

- **云基础架构或内部部署上的Adobe Commerce：**&#x200B;可用于Adobe Commerce 2.4.4及更高版本的实时搜索语义搜索。 在“管理员”中，转到“营销”>“SEO和搜索”>“实时搜索”，打开“设置”，启用语义搜索并保存。 它支持英语目录。 [设置 — 语义搜索](https://experienceleague.adobe.com/zh-hans/docs/commerce/live-search/live-search-admin/settings)
- **Adobe Commerce as a Cloud Service：**&#x200B;系统默认启用语义搜索。 它支持英语目录。 [语义搜索](https://experienceleague.adobe.com/zh-hans/docs/commerce/live-search/live-search-admin/semantic-search)
- **Adobe Commerce Optimizer：**&#x200B;系统默认启用语义搜索。 您可以选择调整控件，如语义提升和相似度阈值。 这些设置还包括模糊搜索选项。 [语义搜索](https://experienceleague.adobe.com/zh-hans/docs/commerce/optimizer/setup/semantic-search) · [设置 — 可选调整](https://experienceleague.adobe.com/zh-hans/docs/commerce/optimizer/settings)

## 将搜索见解转化为行动

使用连续的审查周期来改进产品发现：

1. **查找要调查的查询。** 查看零结果搜索、热门查询和低参与度搜索。
2. **检查购物者要什么。** 确定查询是否指向缺少的产品、措辞不匹配或不清楚的产品数据。
3. **改进产品信息。** 使产品属性和描述对购物者使用的术语准确而有用。 对于Live Search，Adobe建议设置适当的可搜索属性和权重，并确保属性数据相关。 [实时搜索最佳实践](https://experienceleague.adobe.com/zh-hans/docs/commerce/live-search/best-practice)
4. **优化搜索体验。** 在适当时，使用搜索规则、同义词和Facet帮助购物者查找并缩小相关结果。 [实时搜索最佳实践](https://experienceleague.adobe.com/zh-hans/docs/commerce/live-search/best-practice)
5. **查看结果并重复。** 在进行更改后，监测相同的查询和性能信号，然后根据购物者的行为进行调整。

## 使每个搜索都可计数

搜索查询是购物者想要什么的信号。 通过将搜索性能洞察与相关的产品信息和正确的搜索功能配对，您可以使购物者更轻松地发现满足其需求的产品。

### 了解详情

- [什么是Live Search？](../../../live-search/overview.md)
- [实时搜索最佳实践](../../../live-search/best-practice.md)
- 云基础架构上Adobe Commerce的[语义搜索](../../../live-search/semantic-search.md)
- Adobe Commerce Optimizer的[语义搜索](../../../optimizer/setup/semantic-search.md)
