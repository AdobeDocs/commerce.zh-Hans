---
title: 创建和管理同义词
description: 了解如何创建和管理 [!DNL Adobe Commerce Optimizer]的同义词。
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目(Adobe管理的SaaS基础架构)。"
exl-id: d2982a0b-e7df-44e6-b3c9-9b4328635d38
source-git-commit: c6725fc524e9d239ccc0f16701e92ad5d2fc7729
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 0%

---

# 创建同义词

通过添加您自己策划的[!DNL Adobe Commerce Optimizer]同义词列表来提高客户参与度。 每个存储最多可添加200个同义词。

![同义词Workspace](../../assets/synonym-workspace.png)

## 步骤1：添加同义词

1. 从左边栏转到&#x200B;_促销_ > **同义词**。
1. 单击&#x200B;**[!UICONTROL Add synonyms]**&#x200B;按钮。

## 步骤2：按类型定义同义词

按照要创建的同义词[类型](type.md)的说明进行操作。

### 双向同义词

1. 接受默认的&#x200B;**双向**&#x200B;选项。

   ![添加双向同义词](../../assets/synonym-add-two-way.png)

1. 输入要匹配的&#x200B;**关键字**&#x200B;词或短语。
1. 输入要作为关键字的同义词添加的&#x200B;**扩展**&#x200B;术语。 用逗号分隔多个术语。
在此示例中，要匹配的关键字是“pants”，而扩展术语集是“trousers， slacks”。

   ![双向同义词示例](../../assets/synonym-add-two-way-example.png)

1. 完成后，单击&#x200B;**保存**。

   该同义词集显示在列表中，每个术语之间有一个双向箭头，这意味着术语可以互换。

   ![双向同义词](../../assets/synonym-two-way.png)

### 单向同义词

1. 单击&#x200B;**单向**&#x200B;同义词类型。

   ![添加单向同义词](../../assets/synonym-add-one-way.png)

1. 输入&#x200B;**关键字**&#x200B;和&#x200B;**扩展**&#x200B;术语。 用逗号分隔多个术语。

   ![单向同义词示例](../../assets/synonym-add-one-way-example.png)

   在此示例中，关键字是“pants”，而单向扩展术语“capris， peddle-pushers”是“pants”的子集，但具有特定含义。

1. 完成后，单击&#x200B;**保存**。

   同义词集合出现在列表中，有一个从展开项指向关键字的单向箭头，指示这些项是关键字的子集。 每个扩展项之间用加号隔开。

   ![单向同义词](../../assets/synonym-one-way.png)

## 步骤3：发布更改

1. 同义词完成时，单击&#x200B;**发布**。
1. 等待长达两个小时，您的更新才会在店面中出现。

## 字段描述

| 字段 | 描述 |
|--- |--- |
| [类型](type.md) | 确定同义词与关键字的含义相同，还是关键字的子集。 选项：<br />双向（默认） — 与关键字具有相同含义并返回相同搜索结果的术语<br />单向 — 是关键字的子集的术语。 单向同义词返回的特定产品列表更窄。 |
| 关键词 | 通常与目录中的一系列产品相关的单词。 |
| 扩展 | 与关键字具有相同或相似含义的其他术语。 |

## 管理同义词

按照这些说明管理现有[!DNL Adobe Commerce Optimizer] [同义词](overview.md)。

## 查找同义词

为了便于查找同义词，您可以按类型过滤列表并按关键字或扩展词搜索。 这些方法可单独使用，也可同时使用。

1. 要筛选列表，请将&#x200B;**Type**&#x200B;设置为以下项之一：

   - 全部
   - 单向
   - 双向

1. 要搜索关键字或扩展词，请在&#x200B;**[!UICONTROL Search]**&#x200B;框中至少输入三个字符。

## 编辑同义词

1. 查找要编辑的同义词，然后单击&#x200B;**更多** (...)选项。

1. 单击&#x200B;**编辑**。
关键字是列表中的第一个术语，每个术语用逗号分隔。 关键字和扩展词可以更新，但同义词的类型不能更改。
1. 单击要编辑的项目。 然后，根据需要更新文本。

1. 完成后，单击&#x200B;**保存**。

## 删除同义词

1. 在列表中查找要删除的同义词，然后单击&#x200B;**更多** (...)选项。
1. 单击&#x200B;**删除**。
1. 出现提示时，单击&#x200B;**删除同义词**&#x200B;进行确认。

## 发布更改

要完成此过程，必须将保存的更改发布到店面。 更新最多可能需要两个小时才能正式启用。

1. 单击&#x200B;**发布**。
1. 在页面顶部查找用于确认您的更改已发布的消息。
