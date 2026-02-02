---
title: 将数据与SaaS数据导出同步
description: 了解 [!DNL SaaS Data Export] 如何在Adobe Commerce实例和连接的SaaS服务之间收集并同步数据。
role: Admin, Developer
exl-id: 2ca7c92a-fb52-4055-ae16-11e99b38d161
source-git-commit: ea425b56fe7afd9bdaa813d040ac9e47b7022908
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 0%

---

# 将数据与SaaS数据导出同步

当您安装需要数据导出的Commerce服务（如“目录服务”、“实时搜索”或“产品推荐”）时，将安装一组Saas数据导出模块以管理数据收集和同步过程。

SaaS数据导出会持续将产品数据从Adobe Commerce实例移动到Commerce Services平台，以使数据保持最新。 例如，产品推荐需要最新的目录信息才能准确地返回具有正确名称、定价和可用性的推荐。 使用[数据管理仪表板](https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/data-services/catalog-sync)观察和管理同步过程，或者使用命令行界面触发同步并重新索引产品数据以供Commerce服务使用。

下图显示了SaaS数据导出流程。

适用于Adobe Commerce的![SaaS数据导出收集和同步流程](assets/data-export-flow.png){width="900" zoomable="yes"}

SaaS数据导出流的主要组件包括：

- SaaS数据导出模块，用于从Adobe Commerce收集馈送数据、汇编馈送项目、侦听更新并保留馈送状态。
- SaaS导出模块，用于导出数据、配置路由并将馈送发布到连接的服务。
- Adobe Commerce服务可管理数据摄取过程，以验证传入馈送并将更新保留到连接的服务。

>[!NOTE]
>
>为了确保顺利计划并避免站点操作中断，Adobe建议在开始任何数据馈送同步之前估计数据量和同步时间。 在计划初始同步或大规模目录更新（如批量价格更改）时，此估计很重要。 有关详细信息，请参阅[估算数据同步的数据量和传输时间](estimate-data-volume-sync-time.md)

## 同步模式

SaaS数据导出有两种模式来处理实体馈送：

- **立即导出模式** — 在此模式下，将在单个迭代中收集数据并立即将其发送到Commerce服务。 此模式可加快将实体更新交付到Commerce服务的速度，并减小信息源表的存储大小。

- **旧版导出模式** — 在此模式下，将在单个进程中收集数据。 然后，cron作业将收集的数据发送到连接的商务服务。 在数据导出日志条目中，使用旧模式的馈送被标记为`(legacy)`。

## 同步类型

SaaS数据导出支持三种同步类型：完全同步、部分同步和重试失败的项同步。

### 完全同步

将Adobe Commerce实例连接到Commerce服务后，执行完全同步以将实体馈送数据从Adobe Commerce发送到连接的服务。

>[!NOTE]
>
>完全同步主要用于载入阶段。 避免常规使用，以防止数据库过载。 初始同步后，使用部分同步自动同步正在进行的更改。

### 部分同步

通过部分同步，SaaS数据导出会自动将Commerce应用程序中的更新（例如产品名称更改或价格更新）发送到连接的商务服务。

数据导出过程使用以下cron作业来自动执行部分同步操作。

- “索引”cron组作业：
   - `indexer_reindex_all_invalid`作业将重新索引所有无效馈送。 这是标准的Adobe Commerce cron作业。
   - `saas_data_exporter`作业适用于旧版导出源。
   - `sales_data_exporter`作业特定于销售数据导出馈送。

这些作业每分钟运行一次。

为了使部分同步正常工作，Commerce应用程序需要以下配置：

- [已通过cron作业启用任务计划](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html?lang=zh-Hans)

- 所有SaaS数据导出索引器均在`Update by Schedule`模式下配置。

  在SaaS数据导出版本103.1.0及更高版本中，`Update by Schedule`模式默认处于启用状态。 可以使用Commerce CLI命令`bin/magento indexer:show-mode | grep -i feed`验证服务器上的索引配置

### 重试失败的项目同步

重试失败项目同步使用单独的进程来重新发送由于同步过程中出现的错误（例如应用程序错误、网络中断或SaaS服务错误）而未能同步的项目。 此同步的实施也基于cron作业。

- `resync_failed_feeds_data_exporter` cron组作业：
   - `<feed name>_feed_resend_failed_feeds_items`作业重新发送同步失败的项，例如`products_feed_resend_failed_items`。

### 查看和管理同步过程

大多数同步活动是根据应用程序配置自动处理的。 但是，SaaS数据导出还提供了用于监视和管理该过程的工具。

- [!BADGE 仅限PaaS]{type=Informative url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于云项目(Adobe管理的PaaS基础架构)和内部部署项目上的Adobe Commerce 。"} **[数据管理仪表板](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)** — 管理员用户可以查看和跟踪同步到Commerce服务并且可供店面服务使用的数据。

- [!BADGE 仅限SaaS]{type=Positive url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="适用于与Adobe Commerce Optimizer集成的Adobe Commerce项目(Adobe管理的SaaS基础架构)。"} **[数据同步页面](https://experienceleague.adobe.com/zh-hans/docs/commerce/optimizer/setup/data-sync)** — 对于使用[!DNL Adobe Commerce Optimizer]的Commerce项目，请从Adobe Commerce Optimizer的“数据同步”页面检查店面的目录数据可用性。

### 验证Commerce应用程序配置

仅当Commerce实例配置正确时，“部分同步”和“重试失败的项”同步才能正常工作。 通常，在设置Commerce服务时完成配置。 如果数据导出无法正常工作，请检查以下配置。

- [确认cron作业正在运行](https://experienceleague.adobe.com/zh-hans/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues)。

- 验证索引器是从[Admin](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/systems/tools/index-management)运行，还是使用Commerce CLI命令`bin/magento indexer:info`运行。

- 验证以下源的索引器是否设置为`Update by Schedule`：目录属性、产品、产品覆盖和产品变体。 您可以在管理员中或使用CLI ([)从](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/systems/tools/index-management)索引管理`bin/magento indexer:show-mode | grep -i feed`检查索引器。

### 数据传输日志记录的事件管理器通知

在版本103.3.4及更高版本中，当数据从Commerce实例发送到Adobe Commerce服务时，SaaS数据导出会调度`data_sent_outside`事件。

```php
$this->eventManager->dispatch(
   "data_sent_outside",
   [
       "timestamp" => time(),
       "type" => $metadata->getFeedName(),
       "data" => $data
   ]
);
```

>[!NOTE]
>
>有关事件以及如何订阅这些事件的信息，请参阅Adobe Commerce开发人员文档中的[事件和观察者](https://developer.adobe.com/commerce/php/development/components/events-and-observers)。
