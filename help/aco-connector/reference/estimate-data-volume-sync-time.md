---
title: 估计数据量和同步时间
description: 了解如何估算 [!DNL Adobe Commerce Optimizer Connector] 馈送的数据量和同步时间，以计划目录同步并避免中断。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="仅限PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于云项目（Adobe管理的PaaS基础架构）和内部部署项目上的Adobe Commerce 。"
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2: id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: c32adafa-ed01-4b31-997e-2413013911b0
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 469
ht-degree: 0%

---


# 估计数据量和同步时间

Adobe建议在开始任何馈送同步之前估计数据量和同步时间，以确保顺利计划并避免站点操作中断。 在计划初始同步或大规模目录更新（如批量价格更改）时，这一点尤其重要。

缺省情况下，连接器以单线程模式处理馈送。 信息源提交过程无法并行化。 摄取API每秒最多接受2个请求。 但是，[!DNL Adobe Commerce Optimizer]摄取率的基本分配将吞吐量限制为：

- 每分钟最多1,000个产品（产品是具有特定商店视图中的属性的SKU）。 有关基本分配详细信息，请参阅[限制和边界](../../optimizer/boundaries-limits.md)。
- 每分钟高达50,000个价格

## 影响同步时间的因素

以下估计乃基于下列条件而作出：

- 线程计数： 1（默认）
- 馈送接受率：每秒2个请求（每个请求0.5秒）
- 所有产品均已分配到所有现有网站

实际传输速度因请求负载大小和Commerce应用程序服务器上的当前负载而异。

## 计算每个馈送的同步时间

使用下表估计每个连接器信息源的记录数、请求数和同步时间。 批量大小值反映了[支持的馈送](connector-reference.md#supported-feeds)参考中定义的限制。

>[!NOTE]
>
>产品同步时间基于每分钟1,000个产品的基本分配限制。 对于其他馈送，计算基于每秒2个请求的传输速率。 实际速度取决于有效负载大小和服务器负载。
>
>该价格估计假定所有客户组都具有独特的价格。

| 信息源 | 数据示例 | 公式 | 预测的请求 | 预测的同步时间 |
| ---- | ------------ | ------- | ------------------ | ------------------- |
| 产品 | 产品(P)：10,000，商店查看次数(SV)：4 | P × SV = 40,000条记录 | 40,000 ÷批次大小(100) = 400 | 40,000 ÷ 1,000条记录/分钟= **40分钟** |
| 类别 | 类别(C)：500，存储查看次数(SV)：4 | C × SV = 2,000条记录 | 2,000 ÷批次大小(100) = 20 | （20 × 0.5秒） ÷ 60 = **~10秒** |
| 产品属性 | 属性(A)：200，存储视图(SV)：4 | A × SV = 800条记录 | 800 ÷批次大小(100) = 8 | (8 × 0.5 s) ÷ 60 = **~4 s** |
| 价格 | 产品(P)：10,000，网站(WS)：2，客户组(CG)：6 | P × WS × CG = 120,000条记录 | 120,000 ÷批次大小(500) = 240 | （240 × 0.5秒） ÷ 60 = **2分钟** |
| 价格手册 | 网站(WS)：2，客户组(CG)：6 | WS × CG = 12条记录 | 12 ÷批次大小(500) = 1 | （1 × 0.5秒） ÷ 60 = **&lt; 1 s** |

>[!MORELIKETHIS]
>
> - [连接器模块和馈送端点](connector-reference.md) — 查看批次限制和支持的馈送
> - [管理同步](../data-sync-manage.md) — 监视同步状态并触发手动重新同步
> - [连接器同步管道](../connector-sync-pipeline.md) — 了解cron计划和自动同步的工作方式
