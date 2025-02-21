---
title: 添加Facet
description: 了解如何将可筛选的产品属性添加为 [!DNL Live Search] Facet。
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 0%

---

# 添加Facet

任何可过滤的产品属性都可以用作Facet。 *添加Facet*&#x200B;面板列出了当前的Facet，并可轻松地将其他产品属性分配为Facet。 在此三步流程中，选择某个属性作为Facet，根据需要编辑属性，并将更改发布到店面。

![添加Facet](assets/facets-add.png)

## 步骤1：添加方面

1. 在管理员中，转到&#x200B;**营销** > SEO和搜索> **[!DNL Live Search]**。
1. 在&#x200B;*彩块化*&#x200B;选项卡上，单击&#x200B;**添加彩块化**。
1. 在&#x200B;*添加Facet*&#x200B;列表中，每个可用属性都有一个单独的![添加按钮](assets/btn-add.png)。 完成以下任一操作：

   * 在&#x200B;*彩块化属性*&#x200B;列表中，选择要用作Facet的产品属性，然后单击&#x200B;**添加**。
   * 要查找特定的产品属性，请在&#x200B;*搜索*&#x200B;框中输入属性名称的前几个字符。 然后，单击&#x200B;**添加**。

     要配置价格分面间隔和分组，请参阅[设置](settings.md)。 若要了解详细信息，请转到[Facet类型](facets-type.md)。
该Facet已添加到*动态Facet*&#x200B;列表的底部，*发布更改*&#x200B;按钮变为可用。

1. 如果找不到要添加的Facet，请转到&#x200B;**商店** >属性> **产品**，并验证该属性是否具有要用作Facet的[必需属性](facets.md)。 如有必要，请更新属性的以下店面属性：

   * 在搜索中使用 — `Yes`
   * 在搜索结果分层导航中使用 — `Yes`
   * 在分层导航中使用 — `Filterable (with results)`

1. 出现提示时，刷新缓存。

   下次将目录与[!DNL Live Search]同步时，Facet将在店面中变得可用。 如果Facet在两个小时后不可用，请参阅[同步目录数据](install.md#synchronize-catalog-data)。

## 步骤2：编辑Facet属性（可选）

1. 要编辑Facet属性，请单击最右侧列中的&#x200B;**更多** （![更多选择器](assets/btn-more.png)）选项。
1. 在菜单上，单击&#x200B;**编辑**。 然后，根据需要调整以下属性。

   * 标签 — （仅限[Headless](facets-type.md)）输入要使用的Facet标签。
   * 排序类型 — Facet按字母顺序对所有[!DNL Commerce]店面排序。 对于Headless实施，Facet可以按字母顺序或计数排序。 选项：按字母顺序、计数（仅限Headless）
   * 最大值 — 输入店面中显示的最大Facet值数。 有效条目： 0 - 100；默认值： 8

1. 完成后，单击&#x200B;**保存**。

   ![编辑Facet](assets/facet-edit.png)

1. 若要将Facet固定到&#x200B;*筛选器*&#x200B;列表的顶部，请单击灰色图钉（![Pin选择器](assets/btn-pin-gray.png)）。
1. 若要更改固定彩块化的顺序，请单击&#x200B;**移动** （![移动选择器](assets/btn-move.png)）图标，并将该行拖动到&#x200B;*固定彩块化*&#x200B;分区中的新位置。

## 步骤3：发布更改

1. Facet完成后，单击&#x200B;**发布更改**。
1. 等待Facet出现在商店中。
如果Facet在两个小时后不可用，请参阅安装说明中的[验证导出](install.md#synchronize-catalog-data)。

## 字段描述

| 字段 | 描述 |
|--- |--- |
| 标签 | （仅限[Headless](facets-type.md)）可以编辑店面中显示的[Facet标签](facets-type.md)，以便与您的品牌保持一致。 |
| 排序类型 | 用于[排序](facets-type.md)方面的方法。 所有[!DNL Commerce]店面仅按字母顺序对Facet进行排序。 Headless实施也可以按`Count`排序。 选项：<br />按字母顺序 — 按字母顺序对Facet进行排序。<br />计数 — （仅限Headless）根据找到的匹配数对Facet进行排序。 |
| 最大值 | 可在店面中显示的每个Facet的最大值数。 表示一组值的多面均匀分布。 有效条目： 0 - 100；默认值： 8 |

### 控件

| 控件 | 描述 |
|--- |--- |
| ![Pin选择器](assets/btn-pin-blue.png) | 将Facet固定或取消固定到&#x200B;*筛选器*&#x200B;列表的顶部。 |
| ![更多选择器](assets/btn-more.png) | 显示一个菜单，其中包含可应用于选定小平面的更多操作。 选项：编辑、删除 |
| ![移动选择器](assets/btn-move.png) | 使用&#x200B;*移动*&#x200B;图标将固定多面拖动到&#x200B;*固定多面*&#x200B;分区中的其他位置。 |
