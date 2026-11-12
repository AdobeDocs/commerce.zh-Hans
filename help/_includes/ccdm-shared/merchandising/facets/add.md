---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%
---
任何可过滤的产品属性都可以用作Facet。 Facet可帮助客户更轻松地在您的商店中过滤和查找产品。 本文介绍了如何在店面中添加、管理和配置Facet。

![创建Facet](/help/assets/ccdm-shared/facets/create-facet.png)

## 创建方面

1. 从菜单中选择&#x200B;_促销_ > **彩块化**，然后单击&#x200B;**创建彩块化**。
1. 在&#x200B;*创建Facet*&#x200B;列表中，每个可用属性都有一个单独的![添加按钮](/help/assets/ccdm-shared/facets/btn-add.png)。 完成以下任一操作：

   - 在&#x200B;*Facets属性*&#x200B;列表中，选择要用作Facet的产品属性，然后单击&#x200B;**添加**。
   - 要查找特定的产品属性，请在&#x200B;*搜索*&#x200B;框中输入属性名称的前几个字符。 然后，单击&#x200B;**添加**。

   该Facet已添加到&#x200B;*动态Facet*&#x200B;列表的底部，并且&#x200B;*发布更改*&#x200B;按钮变为可用。

1. 如果找不到要添加的Facet，请使用[元数据API](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata){target="_blank"}设置`filterable`参数：

   `"filterable": true`

   下次将目录与Merchandising Services数据层同步时，该Facet将在店面中变得可用。 如果Facet在两个小时后不可用，请参阅[数据同步](../../setup/data-sync.md)。

## 编辑Facet属性（可选）

1. 查找要编辑的方面。
1. 单击（![更多选择器](/help/assets/ccdm-shared/recommendations/btn-more.png)）更多选择器。
1. 在菜单上，单击&#x200B;**编辑**。 然后，根据需要调整以下属性：

   - 标签 — 输入要使用的小平面标签。
   - 排序类型 — 选择下列选项之一：
     - 按字母顺序 — 按字母顺序排序多面
     - 计数 — 根据找到的匹配数对方面进行排序
   - 最大值 — 输入店面中显示的最多多面值。 有效条目： 0 - 100；默认值： 8。

1. 完成后，单击&#x200B;**保存**。

## 固定/取消固定Facet

点击时pin会更改颜色，用于将Facet移动到&#x200B;*固定的Facet*&#x200B;或&#x200B;*动态Facet*&#x200B;部分。

1. 若要将Facet固定到&#x200B;*筛选器*&#x200B;列表的顶部，请在&#x200B;*动态Facet*&#x200B;列表中查找该Facet，然后单击灰色管脚（![Pin选择器](/help/assets/ccdm-shared/facets/btn-pin-gray.png)）。

   销钉变为蓝色，Facet移到&#x200B;*固定的Facet*&#x200B;部分。

1. 若要取消固定Facet，请在&#x200B;*固定Facet*&#x200B;列表中找到Facet，然后单击蓝色Pin （![固定Facet选择器](/help/assets/ccdm-shared/facets/btn-pin-blue.png)）。

   销钉变为灰色，Facet移至&#x200B;*动态Facet*&#x200B;部分。

>[!NOTE]
>
>如果存在两个具有相同名称的标签，则固定的Facet排序可能会不一致。

## 删除Facet

1. 在列表中找到该Facet，然后单击（![更多选择器](/help/assets/ccdm-shared/recommendations/btn-more.png)）更多选择器。
1. 单击&#x200B;**删除**。
1. 提示确认时，单击&#x200B;**删除Facet**。
发布更改后，将从店面中删除方面。

## 发布更改

1. 若要使用更改更新店面，请单击&#x200B;**[!UICONTROL Publish]**。
1. 等待大约15分钟，让更新显示在您的存储中。

## 其他信息

- 要配置价格分面间隔和分组，请参阅[设置](../../settings.md)。
- 了解有关Facet的[类型](type.md)的详细信息。
