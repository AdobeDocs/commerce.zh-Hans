---
title: 管理 [!DNL Adobe Commerce Optimizer Connector] 同步
description: 了解如何验证 [!DNL Adobe Commerce] 和 [!DNL Adobe Commerce Optimizer]之间的目录数据同步和手动重新同步连接器馈送。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="仅限PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于云项目（Adobe管理的PaaS基础架构）和内部部署项目上的Adobe Commerce 。"
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
subfeature_v2:
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 287
ht-degree: 0%

---

# 管理与[!DNL Commerce Optimizer]的同步

设置[!DNL Adobe Commerce Optimizer Connector]后，大多数目录更新都会通过计划的cron作业自动同步。 有关自动同步如何工作的详细信息，请参阅[连接器同步管道](connector-sync-pipeline.md)。 使用此主题中的工具验证数据是否达到[!DNL Adobe Commerce Optimizer]，并在需要时手动重新同步馈送。

## 验证数据同步是否正常工作 {#verify-that-the-data-sync-is-working}

{{$include /help/_includes/aco-connector/verify-optimizer-data-sync.md}}

## 手动重新同步数据 {#manually-resync-data}

当部分同步和自动重试不能解决同步问题时，您可以手动重新同步目录数据。 您选择的选项取决于问题的起源位置以及您需要的控制程度。

| 任务 | 选项 | 注释 |
| --- | --- | --- |
| 验证同步状态，并在缺少产品时从上游系统重新同步 | **上游系统重新同步** | 在[!DNL Commerce Optimizer]中，选择&#x200B;**[!UICONTROL Data Sync]**&#x200B;并验证是否显示预期的目录源、产品、价格和属性。 当产品缺失时，使用&#x200B;**[!UICONTROL Data Feed Sync Status]**&#x200B;页面或Commerce CLI从上游[!DNL Adobe Commerce]实例重新同步（请参阅以下行）。 |
| 重新同步选定的连接器源项目失败或有问题 | Commerce管理员中的&#x200B;**[!UICONTROL Data Feed Sync Status]页面** | 从Commerce管理员中监控导出状态并重新同步选定的连接器信息源项目。 请参阅[验证数据同步是否正常工作](#verify-that-the-data-sync-is-working)。 |
| 具有操作控制的目标连接器馈送重新同步 | **Commerce CLI** | 从Adobe Commerce实例运行`saas:resync`以获取连接器信息源。 请参阅[使用Commerce CLI同步源](../data-export/data-export-cli-commands.md)和[支持的源](reference/connector-reference.md#supported-feeds)。 |

>[!MORELIKETHIS]
>
> - [连接器同步管道](connector-sync-pipeline.md) — 了解自动同步、cron计划和错误处理的工作原理
> - [估算数据量和同步时间](reference/estimate-data-volume-sync-time.md) — 计算预期的同步持续时间
> - [疑难解答](troubleshooting.md) — 诊断凭据、同步和范围导出问题
> - [连接器模块和馈送端点](reference/connector-reference.md) — 审核模块、API端点和支持的馈送
