---
title: 推荐过滤器
description: 了解如何使用筛选器来控制哪些产品出现在 [!DNL Adobe Commerce Optimizer] 推荐中。
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和 [!DNL Adobe Commerce Optimizer] 项目（Adobe管理的SaaS基础架构）。"
exl-id: f6100538-23c0-4e90-9834-a895d4707282
source-git-commit: ba445bf33ec9334c853245fce125af12cd244367
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 0%

---

# 筛选产品

[!DNL Adobe Commerce Optimizer]自动将不可配置的默认筛选器应用于推荐单元。 如果您将多个推荐单元部署到页面，则[!DNL Adobe Commerce Optimizer]会过滤掉这些单元中重复的所有产品。 仅使用对重复产品的第一次引用，以便为推荐其他产品腾出空间。 [!DNL Adobe Commerce Optimizer]还会过滤掉任何以前购买过的产品和购物车中的产品。

当您[创建](create.md)推荐单元时，您可以定义用于控制可在推荐中显示哪些产品的过滤器。 这些过滤器基于您定义的一组包含或排除条件。 只有符合所有包含条件的产品才会出现在推荐中。 不建议使用符合任何排除条件的产品。

您可以通过选择每个过滤器页面上的切换来配置多个过滤器，并仅启用所需的过滤器。 这允许您创建过滤器草稿以供将来使用。 每个选项卡上会显示已启用的过滤器的数量。

## 条件

条件可以是静态或动态。

- 静态条件使用现有的产品属性来确定哪些产品可以显示在设备中。 例如，您可以指定只有价格超过$25的库存产品才会出现在单位中。

- 动态条件可关闭购物者的当前上下文，例如当前查看的类别或产品。 例如，在创建要在产品详细信息页面上部署的产品推荐时，您可以创建一个条件，以仅推荐在当前查看的产品相对价格范围内的产品。

### 逻辑运算符

逻辑运算符`AND`和`OR`用于连接多个条件。 如果同时使用包含和排除过滤器，则会先评估包含内容，以确定所有可能推荐的产品，然后从列表中删除与任何排除过滤器匹配的产品。

- `AND` — 加入两个包含过滤条件
- `OR` — 加入两个排除筛选条件

## 筛选器类型

每种过滤类型都针对目录的不同方面，如产品和价格，因此您可以缩小或扩大哪些产品符合套餐条件。 选择与您的促销目标匹配的类型，然后根据需要组合包含和排除条件；下面的子部分描述了每个类型的行为方式以及[!DNL Adobe Commerce Optimizer]如何应用它。

>[!NOTE]
>
>只能推荐与&#x200B;**包含**&#x200B;过滤器匹配的产品，并且删除与&#x200B;**排除**&#x200B;过滤器匹配的任何产品。

### 价格

>[!IMPORTANT]
>
>以下功能处于测试阶段。

价格筛选使用店面的&#x200B;**有效价格簿**&#x200B;的每个产品的&#x200B;**最终计算价格** — 分配给呈现推荐单位的店面的价格簿。 该值反映该价格手册中定义的折扣、促销和特殊定价，而不只是价目表价格。 评估仅使用店面的价格手册；其他店面或价格手册不适用。 如何在目录和[价格手册](../../setup/pricebooks.md)设置中配置映射到店面的价格手册。

#### 如何包含和排除规则使用价格

- **包含规则** — 只有最终价格&#x200B;**与所有**&#x200B;定义的包含条件相匹配的产品才仍然符合条件。 这包括每个启用的包含过滤器（例如，您的价格范围以及任何其他包含规则）。
- **排除规则** — 将从推荐中删除最终价格&#x200B;**与任何**&#x200B;定义的排除条件匹配的产品。

**显示的价格** — 推荐单位中产品的显示价格与该店面价格手册中的&#x200B;**最终价格**&#x200B;相同，因此购物者看到的价格与用于筛选的值相匹配。

#### 设置价格过滤器

1. 在[创建或编辑](create.md)推荐单元时，打开&#x200B;**[!UICONTROL Filter products]**（或转到单元工作流中的&#x200B;_筛选器_&#x200B;步骤）。
1. 选择&#x200B;**[!UICONTROL Inclusions]**&#x200B;或&#x200B;**[!UICONTROL Exclusions]**&#x200B;选项卡，具体取决于您是希望仅允许价格范围内的产品，还是希望阻止价格范围内的产品。 每个选项卡上的徽章会显示已启用该类型过滤器的数量。
1. 在左侧的列表中，选择&#x200B;**[!UICONTROL Price]**。
1. 打开&#x200B;**[!UICONTROL Enable filter]**。

   价格值使用&#x200B;**网站的基本货币**，如页面上所述。

1. 打开&#x200B;**[!UICONTROL Include products based on]** （在&#x200B;**[!UICONTROL Inclusions]**&#x200B;选项卡上）或&#x200B;**[!UICONTROL Exclusions]**&#x200B;选项卡上的等效控件，然后选择&#x200B;**[!UICONTROL Set price range]**。
1. 使用货币符号旁边的字段设置可选&#x200B;**[!UICONTROL Min price]**&#x200B;和/或&#x200B;**[!UICONTROL Max price]**。 您可以键入金额或使用&#x200B;**-**&#x200B;和&#x200B;**+**&#x200B;控件来调整值。 如果不需要最小值或最大值，请将绑定留空。 该范围会与店面活跃价格手册中每个产品的最终计算价格进行比较。
1. 完成推荐单元配置，并像往常一样保存或发布，以使过滤器生效。

![价格筛选器](../../assets/filter-price.png)

### 产品

产品筛选器按&#x200B;**SKU**&#x200B;定位单个目录项。 添加一个或多个SKU以仅允许这些产品（**排除项**）或阻止这些产品（**排除项**），使用与[价格筛选器](#price)相同的&#x200B;**[!UICONTROL Filter products]**&#x200B;页面。 您不能在推荐单元中显示已禁用的产品或无法单独显示的产品；无论使用什么过滤器，这些产品都不会出现在店面上。

#### 设置产品过滤器

1. 在[创建或编辑](create.md)推荐单元时，打开&#x200B;**[!UICONTROL Filter products]**（或转到单元工作流中的&#x200B;_筛选器_&#x200B;步骤）。
1. 选择&#x200B;**[!UICONTROL Inclusions]**&#x200B;或&#x200B;**[!UICONTROL Exclusions]**&#x200B;选项卡。 每个选项卡上的徽章会显示已启用该类型过滤器的数量。
1. 在左侧的列表中，选择&#x200B;**[!UICONTROL Product]**。
1. 打开&#x200B;**[!UICONTROL Enable filter]**。

   右侧面板标题反映选项卡，例如&#x200B;**[!UICONTROL Product inclusions]**&#x200B;或排除项的等效选项卡。

1. 在&#x200B;**[!UICONTROL Product SKU]**&#x200B;中，输入SKU并单击&#x200B;**[!UICONTROL Add]**。 重复添加更多SKU。

   在&#x200B;**[!UICONTROL Product SKUs]**&#x200B;下，每个SKU都显示为可移动标记。 单击标记上的&#x200B;**X**&#x200B;删除该SKU，或单击&#x200B;**[!UICONTROL Clear All]**&#x200B;从列表中删除每个SKU。

1. 完成推荐单元配置，并像往常一样保存或发布，以使过滤器生效。

对于&#x200B;**包含**，只能推荐列出了SKU的产品（并且满足其他启用的包含过滤器要求）。 对于&#x200B;**排除项**，不建议列出SKU的任何产品，即使它符合其他条件。

![产品筛选器](../../assets/filter-product.png)

>[!NOTE]
>
>可配置产品的子产品不显示在推荐单元中，因为这些子产品具有&#x200B;_不可见_&#x200B;的可见性。

<!--
### Attribute

You can filter products based on attribute criteria, including attribute values. Selected values use OR logic to either include or exclude products when any of the specified values are found.
-->
