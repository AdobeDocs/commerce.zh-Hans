---
title: SaaS数据导出模块
description: 了解 [!DNL SaaS Data Export] 中包含的Magento模块包及其在数据收集、转换和提交到Adobe SaaS服务中的角色。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Developer
feature: Services
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088bid: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: cc250cf1-34eb-4863-80d0-d170d45ea067
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 111
ht-degree: 0%

---


# SaaS数据导出模块

[!DNL SaaS Data Export]包含两个模块组：第一个用于数据收集和索引，第二个用于HTTP传输和提交。

这些模块处理实体更改检测、馈送索引、数据提取和架构定义。
下表仅提供框架级别的模块；可用模块的完整列表取决于已安装的包。

| 模块 | 用途 | 键类 |
| --- | --- |--- |
| `DataExporter` | 核心框架：索引器、馈送表、哈希、重试、锁定 | `FeedIndexer`, `FeedIndexMetadata`, `FeedMetadataPool`, `FeedLockManager` |
| `QueryXml` | 用于数据收集的基于XML的查询DSL | `QueryFactory`, `QueryProcessor`, `SelectBuilder` |
| `SaaSCommon` | 共享HTTP传输、重试、CLI (`saas:resync`)、重新同步编排 | `ExportFeed`, `SubmitFeed`, `ResyncManager`, `ResyncManagerPool`, `ProgressBarManager` |

要了解这些模块在同步期间如何协同工作，请参阅[SaaS数据导出管道](../sync-overview.md)。

>[!MORELIKETHIS]
>
>- [同步的工作方式](../sync-overview.md)
>- [馈送表架构](feed-table-reference.md)
>- [管理SaaS数据导出扩展](../manage-extension.md)
