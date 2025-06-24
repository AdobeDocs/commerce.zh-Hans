---
title: 分担责任
description: 了解 [!DNL Adobe Commerce Optimizer] 项目中涉及的每一方的安全责任。
role: Admin, Architect, Leader
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目(Adobe管理的SaaS基础架构)。"
source-git-commit: 7c407bfc2becfb0ba6babe5958bcb790c178f406
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# 分担责任的安全性和运营模式

>[!BEGINSHADEBOX]

以下汇总表使用RACI模型来显示Adobe与客户之间分担的安全责任。

**R** — 负责人
**A** — 责任人
**C** — 已咨询
**I** — 已通知

>[!ENDSHADEBOX]

| 任务 | Adobe | 客户 |
| --- | --- | --- |
| 应用Adobe Commerce基础设施补丁程序 | RA | |
| 将修补程序应用到支持服务 | RA | |
| 定义后端来源WAF规则 | RA | |
| 定义后端CDN WAF规则 | RA | |
| 部署后端平台WAF规则 | RA | |
| 部署后端CDN WAF规则 | RA | |
| 修复[!DNL Adobe Commerce Optimizer]中的错误 | RA | I |
| 正在发布[!DNL Adobe Commerce Optimizer]基础结构修补程序 | RA | |
| 扩展（基础架构） | RA | I |
| 集成外部应用程序 | | RA |
| 安装App Builder应用程序 | | RA |
| 测试所有App Builder应用程序的性能 | | RA |
| 自定义App Builder应用程序的主题设置和设计 | | RA |
| 配置后端DNS | RA |  |
| 载入后端CDN | RA |  |
| 支持后端CDN | RA |  |
| 获取后端DNS提供商 | RA | |
| 配置生产和沙盒环境 | A | R |
| 访问Dynamics for Adobe Commerce Optimizer | R | C |
| 解决后端客户安全问题 | RA | I |
| 解决后端CDN安全问题 | RA | |
| 协助Adobe进行安全研究（扫描/审核） | RA | |
| 执行PCI ASV扫描 | RA | I |
| 修复Adobe Commerce Optimizer基础架构PCI扫描 | R | |
| 管理操作系统和平台密钥 | RA | |
| 监控后端安全日志 | RA | |
| 控制客户支持和访问 | A | R |
| Adobe灾难恢复计划以及备份和恢复的年度测试和文档记录 | RA | |
| 灾难恢复计划的年度测试和文档记录 | RA | |
| 调试和问题隔离 | R | R |
| 及时支持调试和问题隔离过程 | R | R |
| 安装Adobe Commerce Optimizer的更新和修补程序 | RA | I |
| 核心Adobe Commerce Optimizer应用程序质量 | RA | |
