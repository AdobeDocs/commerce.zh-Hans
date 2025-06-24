---
title: Recommendations最佳实践
description: 了解可在网站上各个页面上放置推荐的位置，以及针对每种推荐类型的常用标签的建议。
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目(Adobe管理的SaaS基础架构)。"
source-git-commit: 3020386cd051b4453ed6b90d2c694a5bb31dfb24
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# Recommendations最佳实践

Adobe建议在使用推荐时遵循以下准则：

- 使推荐类型多样化。 如果客户反复建议相同的产品，则开始忽略推荐。

- 请勿将相同的推荐部署到购物车页面和订单确认页面。 请考虑将`Most Added to Cart`用于购物车页面，将`Bought This, Bought That`用于订单确认页面。

- 保持网站整洁。 请勿在同一页面上部署三个以上的推荐单元。

- 如果您的商店销售服装，则`More like this`推荐可能会建议与正在查看的产品的性别不匹配的特定于性别的产品。 考虑仅对非服装类别使用此推荐类型。

## 投放位置

有这么多推荐类型可供选择，您应在每个页面上使用哪些？ 如果不确定从何处开始，请尝试以下操作：

| 页面 | 推荐类型 |
|---|---|
| 主页 | `Recommended for you` |
| 产品页面 | `Viewed this, viewed that` |
| 购物车 | `Bought this, bought that` |

您可以跟踪[量度](../../manage-results/recommendation-performance.md)，并根据需要进行调整。 请记住，试验是关键。

## 推荐标签

店面中指定给推荐的标签会影响购物者如何解读其与自己的相关性。 以下标签经常用于每种推荐类型。

| 推荐类型 | 推荐的标签 |
|---|---|
| 查看次数最多<br>添加到购物车的次数最多<br>购买次数最多<br>转化（查看购物车）<br>转化（查看购物车） | 最受欢迎的项目<br>最受欢迎的项目<br>趋势<br>当前最受欢迎的项目<br>最近最受欢迎的项目<br>受此项目(PDP)启发的热门项目<br>最畅销商品<br>您可能对 |
| 为您推荐 | 专为您量身打造<br>为您推荐<br>受您购物趋势启发 |
| 查看了这个项目，也查看了那个项目 | 查看此项目的客户也查看了<br>客户也查看了<br>相关项目 |
| 查看了这个项目，购买了那个项目 | 查看了这个项目的客户最终购买了<br>客户最终购买了<br>其他人查看了这个项目后会购买什么？ |
| 买了这个也买了那个 | 获取您所需要的一切<br>不要忘记这些<br>经常一起购买 |
| 更多此类内容 | 其他类似项目<br>类似于 |
| 通用 | 您可能还喜欢<br>购物者也喜欢<br>类似的选项<br>相关项目 |
| 趋势 | 趋势<br>当前趋势<br>最近趋势<br>热门项目<br>趋势相关产品(PDP) |
| 最近查看的项目 | 最近查看的项目<br>再查看一次 |
