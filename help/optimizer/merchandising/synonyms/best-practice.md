---
title: 同义词最佳实践
description: 了解在您的存储中实施同义词的最佳实践。
role: Admin, Developer
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目(Adobe管理的SaaS基础架构)。"
source-git-commit: 54b300ed89f830c2fe5258ec889302a59decd59f
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# 同义词最佳实践

下面提供了创建同义词时的最佳实践列表。

- 默认情况下，[!DNL Adobe Commerce Optimizer]管理拼写错误。 您可以设置同义词，以包含购物者可能使用的与目录中指定单词不同的单词。 您不希望因为某人正在寻找“沙发”而失去销售，而您的产品却被列为“沙发”。 您可以通过输入客户可能用于查找产品的所有词来捕获广泛的搜索词。 您可以[将同义词设置为单向或双向](add.md#step-2-define-the-synonym-by-type)以改进结果。

- 将品牌名称和缩写映射到其全名，例如“HP”映射到“Hewlett-Packard”，将常用产品昵称映射到“iPhone”映射到“Apple iPhone”。

- 包括特定行业的术语和购物者可能互换使用的术语，例如“运动鞋”和“跑鞋”。

- 根据新的搜索趋势、产品添加和购物者行为定期更新同义词列表。

- 通过分析搜索结果和购物者反馈来测试同义词映射的有效性。 优化映射以提高准确性和相关性。

- 避免使用停用词，因为它们不会使同义词更有意义，而是会增加必须处理的数据量。 [!DNL Adobe Commerce Optimizer]从同义词中过滤出常用英语“停用词”，例如：

  a、an、and、are、as、at、be、but、by、for、if、in、into、is、it、no、not、of、on、or、such、that、the、their、then、there、these、they、this、to、was、will、with

- 不必将单词的单数形式和复数形式都定义为同义词。 如果目录中有单项和复项的混合，则搜索将查找正确的产品集。 例如，如果您在产品名称中使用“pant”一词，而购物者搜索“pants”，则会返回正确的产品集，并提供单词“pant”作为建议。 单词“pant”通常用于时尚行业，有时也用于零售业，尽管复数形式的“pants”在某些领域更常用。 （从技术上讲，“裤子”一词指的是服装中遮住一条腿的部分，这就是为什么你需要用“一条裤子”来遮住两条腿。 ）

- 与目录中术语的使用方式保持一致。 请记住，在使用上可能存在地区性差异，有时会存在行业内的差异。
