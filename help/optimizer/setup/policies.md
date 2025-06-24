---
title: 支持
description: 了解如何在 [!DNL Adobe Commerce Optimizer]中创建和管理策略。
recommendations: noCatalog
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目(Adobe管理的SaaS基础架构)。"
source-git-commit: 356b10704c9e7c7329d3e9c0e10baa15d5142ec0
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 0%

---

# 支持

策略是目录视图中包含的数据访问过滤器，用于进一步优化交付给每个目录视图的数据。 策略可确保将正确的内容发送到正确的目标。 例如，销售点实体商店、市场、广告管道(Google、Facebook、Instagram)。

策略基于产品属性（如品牌、模型或部件类别），并用于定制目录数据以满足特定的业务要求。&#x200B;AEM

## 过滤器

过滤器是策略中强制实施目录分段的机制。 过滤器允许企业根据运营需求定制店面和目录视图，使其适合特定的产品集。 可使用产品属性、运算符和值等标准定义规则或条件，以指示在目录视图或店面中包含或排除哪些产品。

### 过滤器的各个部分

过滤器由以下部分组成：

| 部分 | 描述 | 示例 |
|---|---|---|
| **属性** | 用于筛选的产品属性。 | `part_category` |
| **操作员** | 应用于属性的条件。 | `IN`，`EQUALS`，`CONTAINS` |
| **值源** | 指定值是`STATIC`还是`TRIGGER`。 | `STATIC` [了解更多](#value-source-types) |
| **值** | 满足条件的特定值。 | `brakes, suspension` |

### 示例

具有属性`part_category`、运算符`IN`和值`brakes, suspension`的筛选器可确保策略只筛选并显示具有属性`part_category`且值为`brake`或`suspension`的产品。

### 值源类型

有两种类型的值源： **STATIC**&#x200B;和&#x200B;**TRIGGER**。

**值源**&#x200B;为&#x200B;**STATIC**&#x200B;的策略被视为通用策略。 通用策略定义整个网站的体验。 这意味着目录视图将始终执行该策略。 换句话说，该策略的执行不基于店面上的任何用户交互。

**值源**&#x200B;为&#x200B;**TRIGGER**&#x200B;的策略称为独占策略。 这意味着仅当在API调用的标头中指定触发器时，目录视图才会执行该策略。 在店面，这意味着根据购物者选择的内容来显示信息。 例如，在下图中，有两个下拉菜单：**品牌**&#x200B;和&#x200B;**模型**。

![店面上的触发器值源](../assets/policy-trigger.png)

**品牌**&#x200B;和&#x200B;**模型**&#x200B;是已定义的触发器：

- `AC-Policy-Brand`
- `AC-Policy-Model`

如果购物者单击&#x200B;**品牌**&#x200B;下拉列表，则API调用的标头将包含`AC-Policy-Brand`，该标头配置为仅显示特定于`AC-Policy-Brand`策略的产品。

## 创建策略

在此部分中，您将创建一个新策略。 策略可以是&#x200B;**STATIC**&#x200B;或&#x200B;**TRIGGER**。

### 创建静态策略

1. 在左侧菜单上，打开&#x200B;**[!UICONTROL Catalog]**&#x200B;部分并单击&#x200B;**[!UICONTROL Policies]**。

1. 单击&#x200B;**[!UICONTROL Add Policy]**&#x200B;按钮。

   此时将打开一个新页面，供您填写策略详细信息。&#x200B;AEM

1. 输入策略的名称，例如“Celport部件类别”。

1. 单击&#x200B;**[!UICONTROL Add Filter]**&#x200B;按钮。

   将打开一个对话框供您添加过滤器详细信息。

1. 添加筛选器详细信息。 例如：

   1. **属性** — 输入目录中的属性。 例如，“part_category”。 此名称必须与目录中属性的名称完全匹配。
   1. **运算符** — 选择运算符。 例如，**IN**&#x200B;。
   1. **值Source** — 选择&#x200B;**STATIC**&#x200B;。
   1. **值** — 输入您之前指定的属性中的值。 例如，“刹车，暂停”。&#x200B;AEM这些名称必须与先前指定的属性的值的名称完全匹配。

1. 单击筛选器详细信息对话框中的&#x200B;**[!UICONTROL Save]**&#x200B;按钮。&#x200B;AEM

1. 单击您创建的筛选器旁边的操作点(...)，然后选择&#x200B;**启用**。 在此处，您还可以&#x200B;**编辑**、**禁用**&#x200B;或&#x200B;**删除**&#x200B;筛选器。

   **状态**&#x200B;列显示绿色图标和单词“已启用”。

1. 单击&#x200B;**[!UICONTROL Save]**&#x200B;按钮以保存新策略&#x200B;。 如果该按钮未处于活动状态，请确保通过单击&#x200B;**新建策略**&#x200B;旁边的铅笔图标来添加策略名称。

1. 要验证新策略，请单击“上一步”箭头返回策略列表。&#x200B;AEM您将会看到新策略被列出。

### 创建TRIGGER策略

1. 在左侧菜单上，打开&#x200B;**[!UICONTROL Catalog]**&#x200B;部分并单击&#x200B;**[!UICONTROL Policies]**。

1. 单击&#x200B;**[!UICONTROL Add Policy]**&#x200B;按钮。

   此时将打开一个新页面，供您填写策略详细信息。&#x200B;AEM

1. 输入策略的名称，例如“Celport部件类别”。

1. 单击&#x200B;**[!UICONTROL Add Trigger]**&#x200B;按钮。

   出现&#x200B;**触发器详细信息**&#x200B;对话框。

1. 输入触发器的名称，如&#x200B;**AC-Policy-Brand**。

1. 选择&#x200B;**传输类型**。 **HTTP_HEADER**&#x200B;是目前唯一支持的类型。

1. 单击&#x200B;**[!UICONTROL Save]**&#x200B;按钮以保存触发器。

1. 单击&#x200B;**[!UICONTROL Add Filter]**&#x200B;按钮。

   将打开一个对话框供您添加过滤器详细信息。

1. 添加筛选器详细信息。 例如：

   1. **属性** — 输入目录中的属性。 例如，“part_category”。 此名称必须与目录中属性的名称完全匹配。
   1. **运算符** — 选择运算符。 例如，**IN**&#x200B;。
   1. **值Source** — 选择&#x200B;**TRIGGER**&#x200B;。
   1. **值** — 输入您之前创建的触发器名称(**AC-Policy-Brand**)。

1. 单击筛选器详细信息对话框中的&#x200B;**[!UICONTROL Save]**&#x200B;按钮。&#x200B;AEM

1. 单击您创建的筛选器旁边的操作点(...)，然后选择&#x200B;**启用**。 在此处，您还可以&#x200B;**编辑**、**禁用**&#x200B;或&#x200B;**删除**&#x200B;筛选器。

   **状态**&#x200B;列显示绿色图标和单词“已启用”。

1. 单击&#x200B;**[!UICONTROL Save]**&#x200B;按钮以保存新策略&#x200B;。 如果该按钮未处于活动状态，请确保通过单击&#x200B;**新建策略**&#x200B;旁边的铅笔图标来添加策略名称。

1. 要验证新策略，请单击“上一步”箭头返回策略列表。&#x200B;AEM您将会看到新策略被列出。

按照这些步骤，将创建策略并准备好链接到目录视图以控制产品可见性。
