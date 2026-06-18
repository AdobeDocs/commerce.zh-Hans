---
title: ' [!DNL Adobe Commerce Optimizer Connector]疑难解答'
description: 了解如何解决 [!DNL Adobe Commerce] PaaS集成的 [!DNL Adobe Commerce Optimizer Connector] 凭据、目录同步和范围导出问题。
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="仅限PaaS" type="Informative" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于云项目（Adobe管理的PaaS基础架构）和内部部署项目上的Adobe Commerce 。"
autotag-review: '2026-06-09T19:00:00.000Z'
TQID: 'https://experienceleague.adobe.com/ei86QuJ3nQ2d-6NRoAeJslgDxjGlZRejD-Nx-6SAVdc'
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
source-wordcount: 331
ht-degree: 0%

---

# [!DNL Adobe Commerce Optimizer Connector]疑难解答

使用本指南诊断和解决初始设置、目录馈送同步和范围导出配置期间[!DNL Adobe Commerce Optimizer Connector]的常见问题。 以下部分介绍了凭据和租户验证、数据同步失败以及相关的[!DNL SaaS Data Export]诊断。

## 凭据或租户验证失败

如果`aco:config:init`在凭据验证期间失败：

- 运行`bin/magento aco:config:show` [!DNL Adobe Commerce] CLI命令以验证存储的值。
- 确认租户ID属于用于获取凭据的IMS组织。
- 确认OAuth客户端具有[!DNL Adobe Commerce Optimizer]引入服务所需的作用域（请参阅[获取IMS凭据](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/authentication/#obtain-ims-credentials)）。

## 数据未同步

**检查项目级错误详细信息：**

有关在Commerce管理中打开&#x200B;**[!UICONTROL Data Feed Sync Status]**&#x200B;的步骤，请参阅[验证数据同步是否正常工作](./data-sync-manage.md#verify-that-the-data-sync-is-working)。 选择失败的信息源以查看每个项目的错误详细信息。

有关错误处理的要点：

- 未重试&#x200B;**400个错误**。 检查有效负载中是否有格式错误或缺少必填字段。 请参阅连接器信息源的[字段映射](reference/field-mapping.md)以了解预期格式。
- **5xx错误**&#x200B;由`*_resend_failed_items` cron作业自动重试（每5分钟运行一次）。

**检查作用域配置：**

如果问题仅影响特定目录源（商店视图代码）或价格手册，请检查相应的网站或商店视图是否已禁用同步。 请参阅[自定义Commerce范围导出配置](./get-started.md#customize-the-commerce-scopes-export-configuration)。

**解析时：**

连接器信息源在&#x200B;**[!UICONTROL Data Feed Sync Status]**&#x200B;中显示成功状态，预期的产品、价格和属性显示在[!DNL Commerce Optimizer]的&#x200B;**[!UICONTROL Data Sync]**&#x200B;页面上。

## 配置错误和结果解释

有关错误配置或错误解释同步结果所导致的特定行为的目录（如缺少产品、价格不正确或范围级别的数据差距），请参阅[故障排除方案](troubleshooting/troubleshooting-scenarios.md)。

## [!DNL SaaS Data Export]诊断

有关较低级别的[!DNL SaaS Data Export]诊断（包括日志位置和馈送重新同步命令），请参阅[[!DNL SaaS Data Export] 疑难解答指南](https://experienceleague.adobe.com/en/docs/commerce/saas-data-export/troubleshooting/logging){target="_blank"}。
