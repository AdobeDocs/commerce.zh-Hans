---
title: 管理Facet
description: 了解如何管理现有 [!DNL Live Search] 彩块化。
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---

# 管理Facet

按照以下说明更新现有Facet的属性或更改其在店面中的表示法。

## 配置价格方面分组

请参阅[设置](settings.md)以配置价格分面间隔和分组。

## 编辑Facet

1. 查找要编辑的方面。
1. 如果列表中有许多Facet，请将&#x200B;*筛选依据*&#x200B;设置为以下项之一：

   * 已固定
   * 动态

   若要了解详细信息，请转到[Facet类型](facets-type.md)。

   ![筛选Facet](assets/facets-filter-by-cropped.png)

1. 要编辑方面属性，请单击&#x200B;**更多** (...)选项。
1. 单击&#x200B;**编辑**

   ![编辑选项](assets/facet-edit-menu.png)

1. 要编辑多面标签，请执行下列操作之一：

   * 对于[!DNL Commerce]店面，编辑[属性标签](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/product-attributes.html?lang=zh-Hans)。
   * 对于Headless实施，请单击第一列中的值，然后根据需要编辑文本。

   ![编辑标签](assets/facet-edit-label.png)

1. （仅限Headless）要更改用于对Facet值进行排序的方法，请单击&#x200B;*排序类型*&#x200B;列中的值，然后选择以下选项之一：

   * 按字母顺序
   * 计数

   ![编辑计数](assets/facets-edit-count.png)

1. 在&#x200B;**最大值**&#x200B;列中，设置要在店面中显示的Facet筛选值的最大数量（从0到10）。
1. 完成后，单击&#x200B;**保存**。

   您所做的更改在发布之后才会显示在店面中。

## 固定/取消固定方面

点击时pin会更改颜色，用于将Facet移动到&#x200B;*固定的Facet*&#x200B;或&#x200B;*动态Facet*&#x200B;部分。

1. 若要将Facet固定到&#x200B;*筛选器*&#x200B;列表的顶部，请在&#x200B;*动态Facet*&#x200B;列表中查找该Facet，然后单击灰色管脚（![Pin选择器](assets/btn-pin-gray.png)）。

   销钉变为蓝色，Facet移到&#x200B;*固定的Facet*&#x200B;部分。

1. 若要取消固定Facet，请在&#x200B;*固定Facet*&#x200B;列表中找到Facet，然后单击蓝色Pin （![固定Facet选择器](assets/btn-pin-blue.png)）。

   销钉变为灰色，Facet移至&#x200B;*动态Facet*&#x200B;部分。

   ![固定和动态Facet](assets/facets-pinned-unpinned.png)

>[!NOTE]
>
>如果存在两个具有相同名称的标签，则固定的Facet排序可能会不一致。

## 移动固定方面

>[!NOTE]
>
>仅在Headless实施中支持固定彩块化的排序。 如果需要排序的Facet，请使用[!DNL Live Search] PLP小组件。

通过将行移动到不同的位置，可以更改固定小平面的顺序。 固定的Facet在行的开头有一个&#x200B;*移动*&#x200B;图标（![移动选择器](assets/btn-move.png)）。 与固定多面不同，动态Facet无法移动。

1. 在列表的&#x200B;*固定Facet*&#x200B;部分中查找该Facet。
1. 使用&#x200B;**移动** （![移动选择器](assets/btn-move.png)）图标将行拖动到&#x200B;*固定多面*&#x200B;分区中的新位置。

   发布更改后，重新排序的Facet将显示在店面&#x200B;*筛选器*&#x200B;列表中。

## 删除facet

1. 在列表中找到该Facet，然后单击&#x200B;**更多** (...)选项。
1. 单击&#x200B;**删除**。
1. 提示确认时，单击&#x200B;**删除Facet**。
发布更改后，将从店面中删除方面。

## 发布更改

1. 若要使用更改更新店面，请单击&#x200B;**发布更改**。
1. 等待大约15分钟，让更新显示在您的存储中。
