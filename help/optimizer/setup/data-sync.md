---
title: 数据同步
description: 查看正在从Commerce数据源同步到 [!DNL Adobe Commerce Optimizer]中的目录数据。
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目(Adobe管理的SaaS基础架构)。"
exl-id: c0f4664c-6afc-4762-856b-5e26a865d3a2
source-git-commit: e2c3c8a225b2c56985ba48c7efc9ae2c2d059b2e
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# 数据同步

“**数据同步**”页显示从数据源(现有Commerce目录、产品信息管理(PIM)系统、企业资源规划(ERP)系统等)传输到[!DNL Adobe Commerce Optimizer]的产品数据的同步状态概览。

**数据同步**&#x200B;页面提供了有关店面产品数据可用性的宝贵见解，确保可及时向购物者显示这些数据。

**数据同步**&#x200B;页面位于&#x200B;*安装程序* > **数据同步**。

![数据同步](../assets/data-sync.png)

**数据同步**&#x200B;页包含以下字段：

| 字段 | 描述 |
|--- |--- |
| 目录源 | 同步数据的特定区域设置。 |
| [!DNL Catalog Service] | 显示[!DNL Catalog Service]的最新同步更新、收到的产品总数、搜索字段以及同步产品的表。 |
| 产品发现 | 显示最新的同步更新、收到的产品总数、搜索字段和已同步产品的表以供搜索。 |
| Recommendations | 显示最新的同步更新、收到的产品总数、搜索字段以及Recommendations的同步产品的表。 |
| 过去3小时内收到的产品 | 显示过去三小时内已从目录源转移到Adobe Commerce Optimizer的产品数。 如果您不经常更新目录，此值通常为零。 |
| 目录中的产品总数 | 反映可供Adobe Commerce Optimizer使用的目录产品总数。 |
| 已同步的产品 | 提供有关已同步到Adobe Commerce Optimizer的产品的详细信息。 默认情况下，此表按“上次更新时间”排序。 要查找特定产品，请使用&#x200B;**[!UICONTROL Search by Name or SKU]**&#x200B;字段。 |

## 已同步的产品列表

要查看以JSON格式表示的同步产品的详细信息，请单击同步产品表中产品行上的代码图标![代码链接](../assets/data-sync-details.png)。

![同步产品详细信息](../assets/synced-products.png)

## 重新同步目录数据

如果在&#x200B;**数据同步**&#x200B;页面上看不到特定产品，则需要从上游系统启动重新同步。 但是，请记住，重新同步可能会增加硬件资源的负载。 但是，在以下情况下，可能需要重新同步您的目录：

- 对产品目录进行重大更改时，例如添加新产品、更新产品详细信息或修改类别

- 如果您注意到在店面显示产品数据时出现任何差异或性能问题

>[!IMPORTANT]
>
>完成同步所需的时间因目录大小和更新的数据量而异。

## 监视数据同步状态

对于使用Adobe Commerce作为上游数据源的项目，您可以从Commerce管理员的[数据馈送同步状态页面](../../data-export/data-synchronization.md)监视数据导出过程并启动重新同步操作。

