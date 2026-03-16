---
title: 管理您的应用程序
description: 关联、配置和取消关联App Builder应用程序与您的Commerce实例。
feature: App Builder, Extensibility, Integration
source-git-commit: 4a5174d074a020f6199ed121e0289939612bc5c2
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---


# 管理您的应用程序

应用程序管理器将App Builder应用程序与其Commerce实例关联。 配置表单会根据应用程序的架构动态呈现，因此无需自定义管理员UI开发。 应用程序管理器通过Commerce自动生成的表单来配置设置。

![应用管理](assets/app-management-view.png){width="500" zoomable="yes"}

## 先决条件

在关联应用程序之前，请确保您满足以下条件：

| 要求 | 描述 |
|-------------|-------------|
| **管理员访问权限** | 具有[!DNL App Management]权限的Commerce管理员 |
| **已部署应用程序** | App Builder应用程序已部署到您的组织并准备好连接 |
| **组织访问权限** | 访问部署应用程序的Adobe组织 |

## 教程

观看本视频，了解如何将应用程序与Commerce实例关联并配置设置。

>[!VIDEO](https://video.tv.adobe.com/v/3478944)

## 关联应用程序

关联过程将从Commerce导入网站、商店和商店视图，并在应用程序和Commerce实例之间创建链接。

要将App Builder应用程序链接到Commerce实例，请执行以下操作：

1. 导航到&#x200B;**[!UICONTROL Apps]** > **[!UICONTROL App Management]**。

1. 单击&#x200B;**[!UICONTROL Associate App]**。

   ![关联应用](assets/associate-app.png){width="500" zoomable="yes"}

1. 从列表中选择&#x200B;**[!UICONTROL Project]**。

1. 选择&#x200B;**[!UICONTROL Workspace]**。

1. 单击&#x200B;**[!UICONTROL Associate]**。

   ![应用详细信息](assets/app-details.png){width="500" zoomable="yes"}

>[!WARNING]
>
>如果范围同步失败，则关联仍会完成。 您可以稍后从关联应用程序配置的&#x200B;**[!UICONTROL Manage Scopes]**&#x200B;视图中手动同步作用域。

## 配置设置

在[!DNL App Management]视图中关联应用程序后，通过表单配置其设置：

1. 单击关联应用上的&#x200B;**[!UICONTROL Configure]**。

1. 该表单会显示应用程序的可配置设置。

1. 根据需要修改值。

1. 单击&#x200B;**[!UICONTROL Save]**。

### 特定于范围的配置

当不同的网站、商店或商店视图需要唯一的设置时，请使用特定于范围的配置。 例如，仅为特定区域或商店视图启用某个功能，或者为每个品牌使用不同的设置。 较低作用域的设置将覆盖较高作用域的设置。

要覆盖特定范围级别的全局值，请执行以下操作：

1. 单击&#x200B;**[!UICONTROL Change Scope]**。

1. 从列表中选择一个范围。

1. 修改此范围的值。

1. 单击&#x200B;**[!UICONTROL Save]**。

## 管理范围

从应用程序详细信息屏幕访问&#x200B;**[!UICONTROL Manage Scopes]**&#x200B;以管理应用程序的范围层次结构。

![管理作用域](assets/manage-scopes.png){width="500" zoomable="yes"}

| 操作 | 描述 |
|--------|-------------|
| **[!UICONTROL Add root scope]** | 添加仅适用于应用程序的范围。 |
| **[!UICONTROL Sync Commerce scopes]** | 在添加或更改网站、商店和商店后，从Commerce中刷新它们视图的列表。 |
| **[!UICONTROL Import scopes]** | 从文件批量导入作用域。 |

## 取消与应用程序的关联

当您不再需要某个应用程序连接到Commerce实例时，请取消该应用程序的关联。 例如，您可能需要停用集成、切换到其他工作区或清理测试配置。

>[!WARNING]
>
> 取消关联将删除此实例的所有配置值。 无法撤消此操作。

要从Commerce实例中删除应用程序：

1. 导航到&#x200B;**[!UICONTROL Apps]** > **[!UICONTROL App Management]**。

1. 单击应用程序上的&#x200B;**[!UICONTROL Unassociate]**。

1. 确认操作。

## 相关文档

* [疑难解答 [!DNL App Management]](troubleshooting.md) — 解决与应用程序关联和配置有关的常见问题。
