---
title: '[!DNL SaaS Data Export Guide]'
description: 了解如何为Adobe Commerce SaaS服务使用 [!DNL data export] 扩展，在Adobe Commerce和连接的Commerce服务之间同步数据。
role: Admin, Developer
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---

# [!DNL SaaS Data Export] 指南

[!DNL SaaS data export]在Adobe Commerce实例和连接的Commerce服务之间同步数据。 将Live Search、产品推荐或目录服务添加到Adobe Commerce安装时，将自动安装[!DNL Data export]扩展。

SaaS数据导出收集和导出各种类型的数据，称为&#x200B;_馈送_，用于聚合特定类型的信息。 根据安装的Commerce服务，SaaS数据导出源包括：

- **目录实体源**&#x200B;聚合产品数据。 数据包括产品、产品属性、产品价格、产品变体、类别、类别权限和产品权限。
- **范围馈送**&#x200B;汇总客户组、网站、商店和商店视图的数据。
- **销售订单馈送**&#x200B;汇总订单数据，包括其相关实体，如发票、装运、贷项通知单等。
- **多Source库存馈送**&#x200B;汇总有关库存库存状态物料的数据。

SaaS数据导出是作为PHP扩展提供的。 它支持多种方法来启动和管理数据同步过程。

- **从Admin或命令行手动同步**

   - Commerce管理员中的[数据管理仪表板](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard)提供了同步状态的图形视图。 您可以使用仪表板对所有源执行完全重新同步（_完全同步_）。 但是，Adobe建议仅在首次将Adobe Commerce连接到Commerce服务时执行完全同步。 请参阅[同步进程](data-synchronization.md)。

   - [Adobe Commerce命令行工具](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/config-cli) (CLI)提供了同步特定馈送的命令，并包含用于自定义馈送处理的其他选项。

- **与cron作业的自动同步**

   - [部分数据同步](data-synchronization.md#partial-synchronization-with-cron-jobs) — 当Commerce管理员用户更新实体时，Cron作业会触发部分数据同步。 数据导出过程只将这些更新发送到连接的Commerce服务。 部分同步过程基于MView机制，不需要管理员用户或系统集成商执行任何操作。

   - [同步错误的自动重试](data-synchronization.md#failed-items-sync-for-error-recovery) — 在数据同步过程中发生错误时，Cron作业会触发同步过程的自动重试。

- **导出计划和性能**

   - 开发人员和系统集成商可以估算SaaS数据导出所需的时间，以便在Adobe Commerce和连接的服务之间同步数据。 此估计可帮助计划数据导出处理，以防止站点中断。 请参阅[估算数据量和传输时间](estimate-data-volume-sync-time.md)。

   - 在需要更快地执行同步的情况下，SaaS数据导出提供了自定义选项以提高导出处理性能。 请参阅[提高数据导出性能](customize-export-processing.md)。

- **跟踪数据导出活动并排除其故障** — 使用数据导出和saas-export日志在同步和索引过程中查看同步状态和馈送负载。 请参阅[日志记录和疑难解答](troubleshooting-logging.md)。
