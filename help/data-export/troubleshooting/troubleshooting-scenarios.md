---
title: ' [!DNL SaaS Data Export]的疑难解答方案'
description: 了解如何诊断和解决因配置错误、索引器设置或同步结果解释错误导致的意外 [!DNL SaaS Data Export] 同步行为。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="仅限PaaS" type="Informative" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于云项目（Adobe管理的PaaS基础架构）和内部部署项目上的Adobe Commerce 。"
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
subfeature_v2:
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 84cd0deaecda0790f9f123fc663d4db7b048746b
workflow-type: tm+mt
source-wordcount: 983
ht-degree: 0%

---


# [!DNL SaaS Data Export]的疑难解答方案

本页介绍在使用[!DNL SaaS Data Export]时可能观察到的行为，这些行为通常是由错误配置或错误解释同步结果造成的。 使用以下说明确定根本原因并应用相应的解决方案。

## Commerce服务中缺少可配置或捆绑产品 {#configurable-bundle-missing}

**问题：**&#x200B;可配置或捆绑产品在[!DNL Adobe Commerce]中处于&#x200B;*已启用*&#x200B;状态，但未在店面中返回或在Commerce SaaS服务中显示为&#x200B;*已禁用*&#x200B;状态。

**原因：**&#x200B;复合产品的有效状态取决于其子产品的状态，而不只是父产品的状态。 Commerce SaaS服务反映此计算状态：

- **可配置产品** — 必须至少启用一个产品变体。
- **捆绑产品** — 必须为每个所需的捆绑选项至少启用一个产品。

如果不满足这些条件，则父产品将被视为已禁用，即使其自身状态设置为&#x200B;*已启用*&#x200B;也是如此。

**解决方案：**

- 对于可配置产品，验证是否已启用至少一个关联的简单产品变体，并将其分配给正确的网站和商店视图。
- 对于捆绑产品，请检查每个所需的捆绑选项是否至少具有一个已启用的子产品。 对于所有已禁用的子级，必填选项会导致整个捆绑被视为已禁用。
- 启用相应的子产品后，触发重新同步或等待下一个计划同步，然后在Commerce SaaS服务中确认已更新状态。

## 目录价格规则激活后未更新价格 {#prices-not-updated}

**问题：**&#x200B;使用“计划更新”功能激活目录价格规则后，价格不会更新。 在应用计划的更新后，`commerce-data-export.log`显示`prices`信息源的`synced: 0`。

**原因：**&#x200B;当计划的更新用于目录价格规则时，cron组之间可能会出现争用情况。 `catalog_data_exporter_product_prices`索引器可能在其依赖项`catalogrule_product`索引完成重建之前运行。 因此，价格导出程序会读取陈旧数据，并且不会导出任何更改。

**解决方案：**

此问题的直接解决方法是：将两个cron组配置为按顺序运行以消除争用情况：

1. 转到&#x200B;**[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Advanced]** > **[!UICONTROL System]** > **[!UICONTROL Cron (Scheduled Tasks)]**。
1. 将&#x200B;**[!UICONTROL Use Separate Process]**&#x200B;设置为&#x200B;**[!UICONTROL No]**：
   - 组&#x200B;**[!UICONTROL index]**&#x200B;的Cron配置选项
   - 组&#x200B;**[!UICONTROL staging]**&#x200B;的Cron配置选项
1. 保存后刷新配置缓存。

>[!NOTE]
>
>如果两个组都在进程中运行并依次运行，则较慢的完整重新索引会阻止暂存运行，直到它结束。 对于大型目录，这可能会延迟暂存更新。

## [!DNL Adobe Commerce]与连接的服务之间的目录数据不一致 {#catalog-data-discrepancy}

**问题：**&#x200B;连接的Commerce服务中显示的产品数据（如[!DNL Live Search]或[!DNL Product Recommendations]）与[!DNL Adobe Commerce]中的目录数据不匹配。 例如，产品名称、价格或说明在店面中显示为过时或不正确。

**原因：**&#x200B;触发重新同步后，可能需要长达一小时的时间来更新数据并将其反映在UI组件中。 如果差异持续存在到该窗口之外，则上次同步可能未提取该项目，或者同步未检测到更改，因为信息源数据已标记为最新。

**解决方案：**

1. 从Commerce店面，打开搜索结果。 然后，选择相关产品以打开其详细视图。
1. 复制JSON输出，并确认它与[!DNL Commerce]目录中的内容匹配。
1. 如果内容不匹配，请在目录中对产品进行细微编辑，如添加空格或句点，以强制检测更改。
1. 等待重新同步或触发从CLI或Admin中的[[!UICONTROL Data Feed Sync Status]](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status)页面手动重新同步。

有关[!DNL Product Recommendations]中目录数据的其他疑难解答，请参阅Commerce知识库中的[产品推荐模块疑难解答](https://experienceleague.adobe.com/zh-hans/docs/experience-cloud-kcs/kbarticles/ka-40095)。

## 数据同步未按计划运行 {#sync-not-on-schedule}

**问题：**&#x200B;数据同步未按计划运行，或者未同步任何项目，尽管[!DNL Adobe Commerce]中的产品发生了更改。

**原因：**&#x200B;最常见的原因是cron作业未运行或未在&#x200B;**[!UICONTROL Update by Schedule]**&#x200B;模式下配置索引器。

**解决方案：**

- [确认cron作业正在运行](https://experienceleague.adobe.com/zh-hans/docs/experience-cloud-kcs/kbarticles/ka-39832)。
- 验证以下源的索引器是否设置为&#x200B;**[!UICONTROL Update by Schedule]**：目录属性、产品、产品覆盖和产品变体。 在Commerce管理员中或使用CLI从[[!UICONTROL Index Management]](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/systems/tools/index-management)检查： `bin/magento indexer:show-mode | grep -i feed`。

## 目录同步的状态为失败 {#catalog-sync-failed}

**问题：**&#x200B;目录同步在&#x200B;**[!UICONTROL Data Feed Sync Status]**&#x200B;页面上显示&#x200B;**失败**&#x200B;状态。

**原因：**&#x200B;数据收集或提交阶段出现不可恢复的错误。 常见原因包括API身份验证问题、网络错误或数据验证失败。

**解决方案：**

1. 查看数据导出错误日志，了解有关失败的详细信息。 有关日志格式和扩展日志记录选项，请参阅[查看日志和疑难解答](logging.md)：
   - 数据收集期间出现`var/log/commerce-data-export-errors.log`错误。
   - `var/log/saas-export-errors.log`数据提交过程中出现错误。
1. 如果错误与配置或第三方扩展无关，请[提交支持票证](https://experienceleague.adobe.com/zh-hans/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#support-case)以及相关日志条目。

## 日志显示“操作已跳过 — 进程已锁定”消息 {#process-locked}

**问题：** `commerce-data-export.log`文件包含类似以下内容的条目：

```json
{"feed":"products","operation":"partial sync","status":"operation skipped - process locked by \"full sync(1234)\"", ...}
```

**原因：**&#x200B;这是预期行为，而不是错误。 在完全重新索引或`saas:resync`已在进行时，cron触发的部分同步尝试运行，将显示该消息。 [!DNL SaaS Data Export]扩展使用馈送锁定机制来防止发生冲突的并发同步操作。

**解决方案：**

无需执行任何操作。 运行进程完成并释放锁定后，下一个cron执行将选取并同步所有挂起的更改。 有关锁定机制工作方式的详细信息，请参阅[用于SaaS数据导出的馈送锁定机制](../feed-lock-mechanism.md)。

>[!MORELIKETHIS]
>
> - [查看日志和疑难解答](logging.md)
> - [日志代码引用](log-codes-reference.md)
> - 用于SaaS数据导出的[馈送锁定机制](../feed-lock-mechanism.md)
