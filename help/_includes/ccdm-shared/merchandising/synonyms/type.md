---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%
---
单向同义词和双向同义词扩展了关键字的定义。 有些可以和关键词互换，而另一些表示关键词的子集。

## 双向

双向同义词具有相同的含义并返回相同的搜索结果。 在下面的示例中，以粗体显示的第一个单词是目录中使用的关键字，后面跟有与原始关键字相同含义的单词。 您可以为同一关键字创建一个简单的双向同义词对，或创建多个双向同义词链。

**夹克** ![双向选择器](/help/assets/ccdm-shared/synonyms/two-way.png)外套
**裤子** ![双向选择器](/help/assets/ccdm-shared/synonyms/two-way.png)裤子![双向选择器](/help/assets/ccdm-shared/synonyms/two-way.png)裤子

## 单向

单向同义词是关键字的子集，但具有更具体的含义。 例如，羊毛衫和短裤是裤子，但并非所有裤子都是羊毛衫或短裤。 一种裤子搜索包括羊毛衫和短裤。 不过，搜索短裤不会带来额外费用。

**运动衫** ![单向选择器](/help/assets/ccdm-shared/synonyms/one-way.png)连帽衫
**裤子** ![单向选择器](/help/assets/ccdm-shared/synonyms/one-way.png)斜纹帽![单向选择器](/help/assets/ccdm-shared/synonyms/one-way.png)小腿长裤![单向选择器](/help/assets/ccdm-shared/synonyms/one-way.png)小腿推手

## 多词同义词行为

对于多词同义词，系统将该同义词视为短语。 例如，如果您创建一个双向同义词&#x200B;**餐桌** ![双向选择器](/help/assets/ccdm-shared/synonyms/two-way.png) **餐桌** ![双向选择器](/help/assets/ccdm-shared/synonyms/two-way.png) **餐桌**，则系统将在所有设置为可搜索的字段内搜索&#x200B;**餐桌**&#x200B;或&#x200B;**餐桌**&#x200B;或&#x200B;**餐桌**&#x200B;的出现情况。

如果未创建同义词，并且购物者搜索&#x200B;**kitchen table**，则系统会在可搜索字段的任何位置查找术语，甚至跨不同的字段查找术语，例如，名称字段中的&#x200B;**table**&#x200B;和元关键字中的&#x200B;**kitchen**。

创建同义词后，搜索行为将更改为查找确切短语&#x200B;**厨房表**。 这可能会减少结果的数量，因为只会显示包含精确短语的产品。

如果您希望与以前一样单独搜索术语，您可以[创建支持票证](https://experienceleague.adobe.com/zh-hans/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide)。
