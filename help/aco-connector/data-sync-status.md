---
title: 监控目录数据同步
description: 了解如何验证在[!DNL Adobe Commerce]和[!DNL Adobe Commerce Optimizer]之间通过数据馈送同步状态进行的目录数据同步和手动重新同步连接器馈送。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="仅限PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于云项目（Adobe管理的PaaS基础架构）和内部部署项目上的Adobe Commerce 。"
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
subfeature_v2:
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
    internal-label: Data Transfer
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
    internal-label: Data management
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
last-update: 2026-10-01
source-git-commit: 9ed3a09bc4e26e2ef787909700f51e25de0a18fa
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%
---
# 监控目录数据同步

设置[!DNL Adobe Commerce Optimizer Connector]后，大多数目录更新都会通过计划的cron作业自动同步。 有关自动同步如何工作的详细信息，请参阅[连接器同步管道](connector-sync-pipeline.md)。 使用此主题中的工具验证产品、价格和类别数据是否达到[!DNL Adobe Commerce Optimizer]，并在需要时手动重新同步信息源。

## 验证数据同步是否正常工作 {#verify-that-the-data-sync-is-working}

{{$include /help/_includes/aco-connector/verify-optimizer-data-sync.md}}

## 手动重新同步数据 {#manually-resync-data}

当部分同步和自动重试不能解决同步问题时，您可以手动重新同步目录数据。 您选择的选项取决于问题的起源位置以及您需要的控制程度。

| 任务 | 选项 | 注释 |
| --- | --- | --- |
| 验证同步状态，并在缺少产品时从上游系统重新同步 | **上游系统重新同步** | 在[!DNL Commerce Optimizer]中，选择&#x200B;**[!UICONTROL Data Sync]**&#x200B;并验证是否显示预期的目录源、产品、价格和属性。 当产品缺失时，使用&#x200B;**[!UICONTROL Data Feed Sync Status]**&#x200B;页面或Commerce CLI从上游[!DNL Adobe Commerce]实例重新同步（请参阅以下行）。 |
| 重新同步选定的连接器源项目失败或有问题 | Commerce管理员中的&#x200B;**[!UICONTROL Data Feed Sync Status]页面** | 从Commerce管理员中监控导出状态并重新同步选定的连接器信息源项目。 请参阅[验证数据同步是否正常工作](#verify-that-the-data-sync-is-working)。 |
| 具有操作控制的目标连接器馈送重新同步 | **Commerce CLI** | 运行[!DNL Adobe Commerce]实例中的`saas:resync`以获得连接器源。 请参阅[使用Commerce CLI同步源](../data-export/data-export-cli-commands.md)和[支持的源](reference/connector-reference.md#supported-feeds)。 |

>[!MORELIKETHIS]
>
> - [连接器同步管道](connector-sync-pipeline.md) — 了解自动同步、cron计划和错误处理的工作原理
> - [估算数据量和同步时间](reference/estimate-data-volume-sync-time.md) — 计算预期的同步持续时间
> - [疑难解答](troubleshooting.md) — 诊断凭据、同步和范围导出问题
> - [自定义Commerce作用域导出配置](./get-started.md#customize-the-commerce-scopes-export-configuration) — 按作用域级别配置馈送、启用和禁用行为以及管理步骤
> - [连接器模块和馈送端点](reference/connector-reference.md) — 审核模块、API端点和支持的馈送
> - [Commerce管理员中的“数据馈送同步状态”页面](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status){target="_blank"} — 了解有关可用于监视馈送状态的字段和功能的更多信息
> - [位于 [!DNL Commerce Optimizer]](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/data-sync){target="_blank"}的数据同步仪表板 — 有关可用于监视目录数据同步的字段和操作的参考文档
