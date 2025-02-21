---
title: 同义词的类型
description: 单向 [!DNL Live Search] 和双向同义词扩展了关键字的定义。
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---

# 同义词的类型

单向同义词和双向同义词扩展了关键字的定义。 有些可以和关键词互换，而另一些表示关键词的子集。

## 双向

双向同义词具有相同的含义并返回相同的搜索结果。 在下面的示例中，以粗体显示的第一个单词是目录中使用的关键字，后面跟有与原始关键字相同含义的单词。 您可以为同一关键字创建一个简单的双向同义词对，或创建多个双向同义词链。

**夹克** ![双向选择器](assets/btn-two-way.png)外套
**裤子** ![双向选择器](assets/btn-two-way.png)裤子![双向选择器](assets/btn-two-way.png)裤子

## 单向

单向同义词是关键字的子集，但具有更具体的含义。 例如，羊毛衫和短裤是裤子，但并非所有裤子都是羊毛衫或短裤。 一种裤子搜索包括羊毛衫和短裤。 不过，搜索短裤不会带来额外费用。

**运动衫** ![单向选择器](assets/btn-one-way.png)连帽衫
**裤子** ![单向选择器](assets/btn-one-way.png)卡普里斯![多个单向选择器](assets/btn-multiple-one-way.png)小腿长裤![多个单向选择器](assets/btn-multiple-one-way.png)兜售推手

## 最佳实践

请牢记以下最佳实践，以充分利用[!DNL Live Search]同义词。

### 避免“停用词”

[!DNL Live Search]从同义词中过滤出常用英语“停用词”，例如：

a、an、and、are、as、at、be、but、by、for、if、in、into、is、it、no、not、of、on、or、such、that、the、their、then、there、these、they、this、to、was、will、with

停用词不会使同义词更有意义，而是会增加必须处理的数据量。

### 使用单词

如果同义词包含多个单词，则单词之间的空格会导致将它们视为单独的同义词。 例如，如果将“time piece”定义为“watch”的同义词，则“time”和“piece”将被视为单独的同义词。

### 使用单数和复数

不必将单词的单数形式和复数形式都定义为同义词。 如果目录中有单项和复项的混合，则搜索将查找正确的产品集。 例如，如果您在产品名称中使用“pant”一词，而购物者搜索“pants”，则会返回正确的产品集，并提供单词“pant”作为建议。 单词“pant”通常用于时尚行业，有时也用于零售业，尽管复数形式的“pants”在某些领域更常用。 （从技术上讲，“裤子”一词指的是服装中遮住一条腿的部分，这就是为什么你需要用“一条裤子”来遮住两条腿。 ）

### 一致性

与目录中术语的使用方式保持一致。 请记住，在使用上可能存在地区性差异，有时会存在行业内的差异。
