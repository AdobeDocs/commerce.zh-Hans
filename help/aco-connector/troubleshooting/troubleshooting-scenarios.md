---
title: ' [!DNL Adobe Commerce Optimizer Connector]的疑难解答方案'
description: 诊断并解决 [!DNL Adobe Commerce Optimizer Connector] 中由于错误配置或错误解释同步结果导致的意外行为。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="仅限PaaS" type="Informative" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于云项目（Adobe管理的PaaS基础架构）和内部部署项目上的Adobe Commerce 。"
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
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
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 516
ht-degree: 0%

---


# [!DNL Adobe Commerce Optimizer Connector]的疑难解答方案

本页介绍在使用[!DNL Adobe Commerce Optimizer Connector]时可能观察到的行为，这些行为通常是由错误配置或错误解释同步结果造成的。 使用以下说明确定根本原因并应用相应的解决方案。

## 信息源状态显示为“Success”，但数据在[!DNL Adobe Commerce Optimizer]中不可见

**问题：** **[!UICONTROL Data Feed Sync Status]**&#x200B;页面报告同步成功，但[!DNL Adobe Commerce Optimizer]中未按预期显示产品、价格等。

**原因：**&#x200B;馈送状态成功表示引入终结点已接受数据，而不是该数据已完成通过[!DNL Adobe Commerce Optimizer]传播。 引入后，传播可能需要几分钟时间。

**解决方案：**

- 等待几分钟，然后刷新[!DNL Adobe Commerce Optimizer]视图。
- 确认在[!DNL Adobe Commerce]中配置的租户ID与您正在检查的[!DNL Commerce Optimizer]环境匹配。
- 验证是否在[!DNL Commerce Optimizer]中选择了正确的[目录源](../../optimizer/setup/catalog-sources.md) （商店视图代码）或价格手册。

## 导出目录中缺少产品

**问题：**&#x200B;在完全目录同步后，[!DNL Adobe Commerce Optimizer]中未出现某些产品。

**原因：**&#x200B;如果产品在导出期间验证失败，则同步中会忽略这些产品。 产品API不会返回在目录中禁用或不可见的产品。

**解决方案：**

- 确认已将受影响的产品分配给用作目录源的网站和商店视图。
- 检查产品是否已启用并设置为包括目录列表的可见性。
- 在&#x200B;**[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**&#x200B;中查看目录馈送的每项目错误详细信息。

## [!DNL Adobe Commerce Optimizer]中的价格不正确或缺少

**问题：**&#x200B;产品出现在[!DNL Adobe Commerce Optimizer]中，但显示[产品GraphQL查询](https://developer.adobe.com/commerce/services/reference/graphql/#products){target="_blank"}未返回任何价格，或者价格与[!DNL Adobe Commerce]中配置的价格不匹配。

**原因：**&#x200B;价格手册信息源使用映射到特定网站和客户组的范围。 错误的[目录视图](../../optimizer/setup/catalog-view.md)配置可能会导致价格缺失或不正确。

**解决方案：**

- 验证是否将该网站配置为在连接器的导出配置中进行同步。 请参阅[自定义数据导出配置](../get-started.md#customize-the-commerce-scopes-export-configuration)。
- 确认用于执行产品查询的[目录视图](../../optimizer/setup/catalog-view.md){target="_blank"}配置中存在[!DNL Commerce Optimizer]中使用的价格簿ID。

## 同步后[!DNL Adobe Commerce Optimizer]中的数据被覆盖或意外修改

**问题：**&#x200B;连接器运行同步后，外部系统（如PIM或ERP）直接在[!DNL Adobe Commerce Optimizer]中应用的数据更改丢失或还原。

**原因：**&#x200B;当[!DNL Adobe Commerce]以外的系统直接写入[!DNL Adobe Commerce Optimizer]（例如PIM或其他外部系统）时，可能会发生数据冲突。 连接器将数据&#x200B;*从[!DNL Adobe Commerce]单向同步到[!DNL Adobe Commerce Optimizer]，并且不会将更改同步回[!DNL Adobe Commerce]。*&#x200B;因此，直接写入[!DNL Adobe Commerce Optimizer]的数据不会反映在[!DNL Adobe Commerce]中，因此可以在以后的同步过程中覆盖。


**解决方案：**

使用[目录层](../../optimizer/setup/catalog-layer.md){target="_blank"}在[!DNL Adobe Commerce]外部应用更改，而不是将目录修改直接写入[!DNL Adobe Commerce Optimizer]。 目录层允许外部系统扩充或覆盖[!DNL Adobe Commerce Optimizer]中的目录数据，而不会与连接器同步发生冲突。

## 常见[!DNL SaaS Data Export]问题的疑难解答方案

有关可能影响连接器的基础[!DNL SaaS Data Export]的相关问题，请参阅[针对 [!DNL SaaS Data Export]](../../data-export/troubleshooting/troubleshooting-scenarios.md)的疑难解答方案。
