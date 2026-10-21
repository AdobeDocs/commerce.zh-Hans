---
title: 分担责任
description: 了解[!DNL Adobe Commerce as a Cloud Service]项目中涉及的每一方的安全责任。
feature: Cloud, Security
role: Admin, Developer, Leader
level: Intermediate
exl-id: 424fe5cd-5d54-425d-97ce-024476d18dde
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目（Adobe管理的SaaS基础架构）。"
autotag-review: '2026-06-18T16:19:21.186Z'
TQID: 'https://experienceleague.adobe.com/ZjR9eFTVz8RIrYIN1CxyEgegGoZljXJKrtWZStx-ln0'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
    internal-label: Security
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
subfeature_v2:
  - id: d9ced453-36f4-4eb5-b2f3-1d593e32476b
    internal-label: Account management
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
    internal-label: Customer experience
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
source-git-commit: 8b3db59ed02539646dd53a2e9c7a0925b7c3a804
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%
---
# 分担责任的安全性和运营模式

[!DNL Adobe Commerce as a Cloud Service]是一项按需服务，它依赖于分担责任的安全性和操作模型。 Adobe和客户共同承担这些责任，并且各方对保护和运行Adobe Commerce应用程序承担不同的责任。

[!DNL Adobe Commerce as a Cloud Service with Managed Operations]是一款高级产品，在标准共享责任模型之外还增加了指定客户成功工程师(CSE)和全天候托管操作P1支持团队。 Adobe继续拥有平台、基础架构、安全性和核心应用程序，并且您继续拥有您的自定义和集成，但是通过托管操作，您可在以下方面咨询Adobe Managed Services：

- 集成
- App Builder应用程序
- Edge Delivery店面
- 事件管理
- 平台更新

Adobe Managed Services还共同负责灾难恢复测试、调试和问题隔离。 您的CSE指导您从上线到上线及其后各阶段，因此您在每个阶段都有一位Adobe专家与您联系，而不是依靠您自己的力量运营。

>[!BEGINSHADEBOX]

以下汇总表使用RACI模型来显示Adobe、Adobe Managed Operations和客户之间共享的安全责任。

**R** — 负责人
**A** — 责任人
**C** — 已咨询
**I** — 已通知

>[!ENDSHADEBOX]

| 任务 | Adobe | Adobe托管操作 | 客户 |
| --- | --- | --- | --- |
| 定义后端来源WAF规则 | RA | | |
| 定义后端CDN WAF规则 | RA | | |
| 部署和维护[!DNL Adobe Developer App Builder]个应用程序 | | | RA |
| 部署后端平台WAF规则 | RA | | |
| 部署后端CDN WAF规则 | RA | | |
| 正在修复[!DNL Adobe Commerce as a Cloud Service]中的核心错误 | RA | | I |
| 正在发布[!DNL Adobe Commerce as a Cloud Service]基础结构修补程序 | RA | | |
| 扩展（基础架构） | RA | | |
| 缩放（核心应用程序） | RA | | |
| 集成外部应用程序 | | C | RA |
| 安装App Builder应用程序 | | C | RA |
| 测试所有App Builder应用程序的性能 | | C | RA |
| 自定义App Builder应用程序的主题设置和设计 | | C | RA |
| 配置后端DNS | RA | | I |
| 载入后端CDN | RA | | I |
| 支持后端CDN | RA | | I |
| 获取后端DNS提供商 | RA | | |
| 配置生产和沙盒环境 | A | | R |
| 在云基础架构上访问Dynamics for Adobe Commerce | R | | C |
| 解决后端客户安全问题 | RA | | I |
| 解决后端CDN安全问题 | RA | | |
| 协助Adobe进行安全研究（扫描/审核） | RA | | |
| 执行PCI ASV扫描 | RA | | I |
| 修复Adobe Commerce基础架构PCI扫描 | R | | |
| 管理操作系统和平台密钥 | RA | | |
| 监控后端安全日志 | RA | | |
| 控制客户支持和访问 | A | C | R |
| Adobe灾难恢复计划以及备份和恢复的年度测试和文档记录 | RA | C | |
| 灾难恢复计划的年度测试和文档记录 | RA | RA | |
| 调试和问题隔离 | R | R | R |
| 及时支持调试和问题隔离过程 | R | R | R |
| 将更新和修补程序发布到Adobe Commerce核心 | RA | C | I |
| 安装Adobe Commerce核心的更新和修补程序 | RA | C | I |
| 核心Adobe Commerce应用程序质量 | RA | C | |
