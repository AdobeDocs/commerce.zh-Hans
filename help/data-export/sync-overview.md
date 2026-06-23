---
title: 将数据与SaaS数据导出同步
description: 了解 [!DNL SaaS Data Export] 如何在Adobe Commerce实例和连接的Commerce服务之间收集并同步数据。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: 2ca7c92a-fb52-4055-ae16-11e99b38d161
TQID: https://experienceleague.adobe.com/wM71qxvduDr77EW6Y8mSNfBXlqkloC-PGOOBOl-mZQM
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: ef1a9efc579d8d21c145e6981235489a2e4ea203
workflow-type: tm+mt
source-wordcount: 907
ht-degree: 0%

---

# 将数据与SaaS数据导出同步

当您安装需要数据导出的[!DNL Adobe Commerce]服务（如“目录服务”、“实时搜索”或“产品推荐”）时，将安装SaaS数据导出模块的集合以管理数据收集和同步过程。

SaaS数据导出会持续将产品数据从Adobe Commerce实例移动到Commerce Services平台，以使数据保持最新。 例如，产品推荐需要最新的目录信息才能准确地返回具有正确名称、定价和可用性的推荐。 有关监视同步进程的详细信息，请参阅[查看和管理同步进程](data-sync-manage.md)。

下图显示了SaaS数据导出流程。

适用于Adobe Commerce的![SaaS数据导出收集和同步流程](assets/data-export-flow.png){width="900" zoomable="yes"}

当目录数据在[!DNL Adobe Commerce]中更改时，同步将经过这些阶段。

1. **实体更改检测** - Magento的Mview系统检测订阅的数据库表（例如，`catalog_product_entity`）中的行更改，并将条目写入changelog表。
1. **信息源索引** — 信息源索引器读取更改日志，从源表加载实体数据，并组合信息源项目。
1. **数据收集和转换** — 在馈送架构[`et_schema.xml`](extensibility-and-customizations.md#feed-schema-overview)中注册的提供程序收集字段数据。
1. **哈希去重** — 为每个馈送项计算内容哈希。 跳过自上次导出后散列未发生更改的项目，因此仅传输修改后的数据。
1. **HTTP提交** — 馈送项目将作为经过身份验证的HTTP POST批次发送到Adobe SaaS馈送引入服务。
1. **状态持续存在** - API响应状态将回写到每个项目的[信息源表](reference/feed-table-reference.md)。
1. **失败重试** — 计划的cron作业会自动重试导出失败的项。

>[!NOTE]
>
>对于[!DNL Adobe Commerce Optimizer Connector]部署，[!DNL SaaS Data Export]处理实体更改检测和馈送程序集。 然后，连接器将馈送映射到[!DNL Catalog Data Ingestion API]格式并提交给[!DNL Adobe Commerce Optimizer]。 有关范围控制、提交和错误处理，请参阅[连接器同步管道](../aco-connector/connector-sync-pipeline.md)。

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

>[!NOTE]
>
>`saas:resync`命令仅传输新项目、更新的项目和以前无法导出的项目。 跳过自上次导出以来内容哈希未更改的项目。

### 部分同步 {#partial-sync}

通过部分同步，SaaS数据导出会自动将Commerce应用程序中的更新（例如产品名称更改或价格更新）发送到连接的商务服务。
为了使部分同步正常工作，Commerce应用程序需要以下配置：

- [通过cron作业启用任务计划](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html)
- 所有SaaS数据导出索引器均在`Update by Schedule`模式下配置。

### 重试失败的项目同步 {#retry-failed-items-sync}

重试失败项目同步使用单独的进程来重新发送由于同步过程中出现的错误（例如应用程序错误、网络中断或SaaS服务错误）而未能同步的项目。 `resync_failed_feeds_data_exporter`组中的`*_resend_failed_items` cron作业每5分钟自动处理一次此操作。

## 计划的cron作业

以下cron组按固定计划自动执行管道。

| Cron组 | Cron作业 | 用途 | 计划 |
|---|---|---|---|
| `index` | `indexer_update_all_views` | 处理Mview更改日志并触发部分信息源更新 | 每1分钟 |
| `index` | `indexer_reindex_all_invalid` | 对标记为“需要重新索引”的源索引执行完全重新同步 | 每1分钟 |
| `resync_failed_feeds_data_exporter` | `*_resend_failed_items` | 检测有故障的信息源项目并重新提交它们 | 每5分钟 |
| `commerce_data_export` | `saas_data_exporter` | 为旧模式馈送（订单、范围）提交数据 | 每5分钟 |
| `commerce_data_export` | `cleanup_deleted_feed_items` | 清理超过保留期（7天）的同步删除的信息源项目 | 每天凌晨2:00 |

## 馈送提交和HTTP错误处理 {#feed-submission-and-http-error-handling}

馈送项目会通过HTTP POST以经过身份验证的gzip压缩的JSON批次形式提交。 下表显示了HTTP响应代码如何映射到导出状态和重试行为。

| 状态代码 | 重试？ | 含义 |
|-------------|--------|---------------------------------------------------------------------------------------------------------------------|
| 200 | 否 | 已成功接受 |
| 400 | 否 | 数据错误或验证失败 — 需要手动调查。 有关详细信息，请查看`var/log/saas-export-errors.log`。 |
| 429 | 是 | 达到速率限制 — 在[导出处理设置](customize-export-processing.md)中减少`thread_count` |
| 5xx | 是 | SaaS端错误 — 自动重试 |
| 2 | 是 | 已计划重试项目 |

除了HTTP级失败之外，应用程序级错误（如本地处理失败或网络中断）也计划由`*_resend_failed_items` cron作业自动重试。

从Commerce管理员的[[!UICONTROL Data Feed Sync Status]](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status)页面中监视每个馈送的状态。

>[!MORELIKETHIS]
>
> - [管理同步](data-sync-manage.md) — 验证同步状态并手动重新同步馈送。
> - [信息源表架构](reference/feed-table-reference.md) — 检查项目级别状态和错误详细信息。
> - [提高数据导出性能](customize-export-processing.md) — 调整批次大小和线程计数。
