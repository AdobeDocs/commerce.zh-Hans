---
title: 彩块化Workspace
description: 了解如何在 [!DNL Live Search] 彩块化工作区中运行。
exl-id: 7108e41b-44a7-4943-b20f-6ee544d099e9
TQID: https://experienceleague.adobe.com/LsVM4inUqk2EozfVN--FH1Ukggt8A8QBIQXW-SmnxZs
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 229
ht-degree: 0%

---

# 彩块化Workspace

*彩块化*&#x200B;工作区列出了当前可用的所有Facet，并提供了对设置和管理Facet所需工具的访问权限。 固定多面首先出现在现有Facet列表中，然后是动态Facet。 可以对列表进行过滤，以显示所有方面，或仅显示固定或动态方面。

![彩块化工作区](assets/faceting-workspace.png)

## 设置范围

如果您的Adobe Commerce安装包含多个商店视图，请将&#x200B;**范围**&#x200B;设置为应用您的方面设置的[商店视图](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html?lang=zh-Hans#scope-settings)。

## 筛选列表

1. 单击&#x200B;**筛选依据**&#x200B;控件。
1. 选择下列选项之一：

   * 所有筛选器
   * 已固定
   * 动态

## 添加方面

1. 单击&#x200B;**添加Facet**。
1. 有关详细说明，请参阅[添加Facet](facets-add.md)。

## 列描述

| 列 | 描述 |
|--- |--- |
| （第一列） | 列出购物者可见的[标签](facets-type.md)固定的动态方面。 |
| 排序类型 | Facet值的[排序顺序](facets-type.md)。 所有[!DNL Commerce]店面的Facet按字母顺序排序。 对于[headless]实施，Facet可以按字母顺序或计数排序。 选项：按字母顺序、计数（仅限Headless） |
| 最大值 | 店面中作为过滤器可用的Facet值的数量，最大为10。 |

## 控件

| 控件 | 描述 |
|--- |--- |
| 添加Facet | 打开[方面编辑器](facets-add.md)。 |
| 过滤方式 | 确定列表中显示的[类型的Facet](facets-type.md)。 选项：全部、固定、动态 |
