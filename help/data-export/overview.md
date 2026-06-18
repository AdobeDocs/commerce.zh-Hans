---
title: '[!DNL SaaS Data Export Guide]'
description: 了解如何为Adobe Commerce SaaS服务使用 [!DNL data export] 扩展，在Adobe Commerce和连接的Commerce服务之间同步数据。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: 8a0067ba-90a4-48a6-8276-208d09abe6fc
TQID: https://experienceleague.adobe.com/OHE1GBUEd8hHFPwFlO9fJa3Y0wK2xZ0HOYnwUn0-DSk
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 402
ht-degree: 0%

---

# [!DNL SaaS Data Export] 指南

[!DNL SaaS data export]在Adobe Commerce实例和连接的Commerce服务之间同步数据。 将Live Search、产品推荐、目录服务或[!DNL Adobe Commerce Optimizer Connector]添加到Adobe Commerce安装时，将自动安装[!DNL Data Export]扩展。

>[!NOTE]
>
>如果您安装[!DNL Adobe Commerce Optimizer Connector]，则同一[!DNL Data Export]扩展将从[!DNL Adobe Commerce]中收集目录和定价源。 然后，连接器使用可组合目录数据模型(CCDM)将这些馈送映射并提交给[!DNL Adobe Commerce Optimizer]。 有关设置和架构，请参阅[[!DNL Adobe Commerce Optimizer Connector] 概述](../aco-connector/overview.md)；有关导出后的同步行为，请参阅[连接器同步管道](../aco-connector/connector-sync-pipeline.md)。

SaaS数据导出收集和导出各种类型的数据，称为&#x200B;_馈送_，用于聚合特定类型的信息。 根据安装的Commerce服务，SaaS数据导出源包括：

- **目录实体源**&#x200B;聚合产品数据。 数据包括产品、产品属性、产品价格、产品变体、类别、类别权限和产品权限。
- **范围馈送**&#x200B;汇总客户组、网站、商店和商店视图的数据。
- **销售订单馈送**&#x200B;汇总订单数据，包括其相关实体，如发票、装运、贷项通知单等。
- **多Source库存馈送**&#x200B;汇总有关库存库存状态物料的数据。

SaaS数据导出是作为PHP扩展提供的，支持自动和手动同步：

- **自动同步** — 在连接Commerce服务时进行初始完全同步后，cron作业将使用部分同步和自动重试失败的项目来保持连接的服务为最新状态，无需管理员用户或系统集成商执行任何操作。

- **手动同步** — 从Commerce管理员或[Commerce CLI](data-export-cli-commands.md)运行完全重新同步或重新同步选定的馈送。

- **监控** — 从Commerce管理员的[!UICONTROL Data Feed Sync Status]页面和数据管理仪表板中跟踪馈送的运行状况、状态和投放。 有关验证和重新同步步骤，请参阅[管理同步](data-sync-manage.md)。

有关同步行为、模式和导出流程图，请参阅[同步的工作方式](sync-overview.md)。

SaaS数据导出还提供了用于规划和排除同步过程故障的工具：

- **时间安排和性能** — 估计同步时间以安排处理并避免站点中断，并自定义导出处理以提高性能。 请参阅[估计数据量和传输时间](estimate-data-volume-sync-time.md)和[提高数据导出性能](customize-export-processing.md)。

- **跟踪和故障排除** — 使用数据导出和saas-export日志检查同步状态和馈送负载。 查看[查看日志和疑难解答](troubleshooting/logging.md)。

>[!MORELIKETHIS]
>
> - [扩展和自定义SaaS数据导出馈送](extensibility-and-customizations.md) — 添加或修改馈送数据。
> - [故障排除方案](troubleshooting/troubleshooting-scenarios.md) — 诊断配置错误和意外的同步结果。
> - [发行说明](release-notes.md) — 扩展更新和已知问题。
