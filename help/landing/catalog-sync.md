---
title: 目录同步
description: 了解如何将产品数据从 [!DNL Commerce] 服务器导出到 [!DNL Commerce Services]。
feature: Catalog Management, Data Import/Export, Catalog Service
exl-id: 99f96b93-b036-490c-8c57-40463a0de365
source-git-commit: ae672ed3f2693e2f14e8c7f379e59ef117a34fc3
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---

# 目录同步

>[!NOTE]
>
> “目录同步”功能板现在是“数据管理功能板”。 此改版后的仪表板现在支持[[!DNL Product Recommendations]](../product-recommendations/guide-overview.md) v6.0.0+、[[!DNL Live Search]](../live-search/overview.md) v4.1.0+和[[!DNL Catalog Service]](../catalog-service/overview.md) v1.17+。 客户可以通过更新到其中一项服务的最新版本来获取数据管理功能板。 请在[数据管理功能板](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html?lang=zh-Hans)文档中阅读更多相关信息。 对于尚未升级但仍拥有目录同步功能板的用户，此当前主题仍然适用。

Adobe Commerce使用索引器将目录数据编译到表中。 该进程由[事件](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/index-management.html?lang=zh-Hans#events-that-trigger-full-reindexing)自动触发，例如产品价格或库存级别的更改。

目录同步服务会持续将产品数据从[!DNL Adobe Commerce]实例移动到[!DNL Commerce Services]平台，以使数据保持最新。 例如，[[!DNL Product Recommendations]](/help/product-recommendations/overview.md)需要当前目录信息才能准确返回具有正确名称、定价和可用性的推荐。 使用&#x200B;_目录同步_&#x200B;仪表板观察和管理同步过程或命令行界面以触发目录同步并重新索引产品数据以供[!DNL Commerce Services]使用。 请参阅[SaaS数据导出](../data-export/data-export-cli-commands.md)指南中的&#x200B;_命令行接口引用_。

## 访问目录同步仪表板

要访问目录同步仪表板，请选择&#x200B;**系统** > _数据传输_ > **目录同步**。

使用&#x200B;**目录同步**&#x200B;仪表板，您可以：

- 查看同步状态（**正在进行**，**成功**，**失败**）
- 查看同步的产品总数
- 搜索同步的产品以查看其当前状态
- 按名称、SKU等搜索存储目录。
- 在JSON中查看同步的产品详细信息，以帮助诊断同步差异
- 重新启动同步过程

### 上次同步

报告同步状态：

- **成功** — 显示同步成功的日期和时间以及更新的产品数
- **失败** — 显示尝试同步的日期和时间
- **进行中** — 显示上次成功同步的日期和时间

目录同步过程每小时自动运行一次。 如果在店面中未看到预期的产品，或者这些产品未反映您最近所做的更改，则可以解决[目录同步问题](#resolvesync)。

### 产品已同步

显示从[!DNL Commerce]目录同步的产品总数。 初次同步后，只应同步已更改的产品。

## 重新同步 {#resync}

如果在进行每小时计划同步之前必须启动目录的重新同步，则可以强制进行重新同步。

>[!NOTE]
>
> 强制重新同步会触发整个产品目录的重新同步，这会增加硬件资源的负载。

1. 从&#x200B;_目录同步_&#x200B;仪表板中，选择&#x200B;**设置**。

   将显示&#x200B;_目录同步设置_&#x200B;页。

1. 在&#x200B;_重新同步数据_&#x200B;部分中，单击[!UICONTROL Resync]。

   [!DNL Commerce]在下一个计划同步窗口同步您的目录。 根据目录的大小，此操作可能需要较长时间。

## 已同步的目录产品

**同步的目录产品**&#x200B;表显示以下信息。

| 字段 | 描述 |
|---|---|
| ID | 产品的唯一标识符 |
| 名称 | 产品的店面名称 |
| 类型 | 标识产品类型，例如简单、可配置或可下载 |
| 上次导出 | 上次成功从目录中导出产品的日期 |
| 上次修改时间 | 上次在目录中修改产品的日期 |
| SKU | 显示产品的库存单位 |
| 价格 | 产品的价格 |
| 可见性 | [!DNL Commerce]目录中定义的产品可见性设置 |

## 解决目录同步问题 {#resolvesync}

请参阅[SaaS数据导出指南](../data-export/troubleshooting-logging.md#troubleshooting)中的&#x200B;_日志和疑难解答_。
