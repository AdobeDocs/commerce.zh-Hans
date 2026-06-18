---
title: 用于SaaS数据导出的馈送锁定机制
description: 了解 [!DNL SaaS Data Export] 如何使用馈送锁定来防止同步操作发生冲突，并在并发馈送更新期间保护数据完整性。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Services
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
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 355
ht-degree: 0%

---


# 用于SaaS数据导出的馈送锁定机制

[!DNL SaaS Data Export]扩展使用馈送锁定机制，以防止多个进程尝试同时同步同一馈送时出现争用情况。 例如，当cron触发的重新同步与手动`saas:resync` CLI调用重叠时，可能会发生这种情况。

## 进纸锁的工作原理

每个馈送同步操作（无论是由cron作业还是手动`saas:resync` CLI调用触发）遵循相同的顺序：

1. 进程将尝试获取馈送锁定。 锁定尝试不会受阻，如果锁定已被另一个进程保持，则会立即返回。
1. 如果锁定为&#x200B;**不可用**，将跳过该操作并将其记录下来。

   没有数据丢失。 在当前流程完成后，下一次cron运行将选取挂起的更改。
1. 如果锁定为&#x200B;**acquired**，进程会记录其名称和PID以进行诊断，然后运行同步。
1. 当同步完成或失败时，将无条件释放锁定，以便下一个计划的cron作业可以正常继续。

一次只能有一个同步操作保持馈送锁定，而不管该操作是通过cron启动还是通过CLI启动。 馈送锁定是通过[!DNL Adobe Commerce]的`LockManagerInterface`实现的。 默认后端是MySQL，它使用`GET_LOCK`和`RELEASE_LOCK`函数。 要配置其他锁定提供程序，请参阅[配置锁定提供程序](https://experienceleague.adobe.com/zh-hans/docs/commerce-operations/installation-guide/tutorials/lock-provider){target="_blank"}。

## 预期的日志消息

`commerce-data-export.log`中的以下消息是正常的，并不表示有问题：

```json
{"feed":"products","operation":"partial sync","status":"operation skipped - process locked by \"full sync(1234)\"", ...}
```

当完全重新索引或`saas:resync`已在进行时，cron触发的部分同步尝试运行，则会显示此消息。 跳过的操作不会丢失。 运行进程完成并释放锁定后，下一个cron执行将选取并同步所有挂起的更改。

>[!NOTE]
>
>有关`commerce-data-export.log`中记录的日志格式和操作类型的一般信息，请参阅[查看日志和疑难解答](troubleshooting/logging.md)。

>[!MORELIKETHIS]
>
> - [将数据与SaaS数据导出同步](sync-overview.md)
> - [使用Commerce CLI同步源](data-export-cli-commands.md)
> - [连接器同步管道](../aco-connector/connector-sync-pipeline.md)
> - [配置锁定提供程序](https://experienceleague.adobe.com/zh-hans/docs/commerce-operations/installation-guide/tutorials/lock-provider){target="_blank"}
