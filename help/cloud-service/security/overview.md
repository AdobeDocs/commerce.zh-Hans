---
title: 安全性概述
description: 了解Adobe Commerce as a Cloud Service的安全功能。
role: Admin, Architect, Leader
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目（Adobe管理的SaaS基础架构）。"
source-git-commit: 0343c4f3ecc182145a97e08eca2790bd1512aa27
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 0%

---


# 安全性概述

[!DNL Adobe Commerce as a Cloud Service]的设计以安全性为核心，提供现代化的SaaS原生商务平台，可为各种规模的企业提供企业级保护、运营恢复能力和高枕无忧。

与传统的PaaS模型不同， SaaS模型消除了手动修补、基础架构维护和升级周期的负担。 安全性嵌入到平台的每个层中 — 从Adobe管理的基础架构和自动部署管道，到通过[!DNL Adobe IMS]进行的身份和访问管理。

[!DNL Adobe Commerce as a Cloud Service]利用Adobe的全球安全和合规框架，确保与ISO 27001、SOC 2和GDPR等行业标准保持一致。 客户从[责任分担模型](./shared-responsibility.md)中受益，该模型清晰地描述了Adobe在保护平台安全方面的角色以及客户在管理数据和访问方面的角色。

通过内置的保护功能(如Web应用程序防火墙(WAF)、减少DDoS、安全配置和持续漏洞扫描)，[!DNL Adobe Commerce as a Cloud Service]使企业能够在不影响安全性的情况下更快地创新。

本文档概述了[!DNL Adobe Commerce as a Cloud Service]的安全体系结构、操作保护措施和法规遵从性状况 — 使客户能够做出明智的决策并放心地扩展其数字商务运营。

## 内容分发网络(CDN)和Web应用程序防火墙(WAF)

### 店面CDN

商家可以选择部署Adobe管理的CDN或购买自己的CDN解决方案来保护他们由Commerce支持的店面。

>[!IMPORTANT]
>
>如果客户选择部署Adobe管理的CDN，则无法配置CDN规则。 客户在自带CDN以保护其店面时，可以配置自定义缓存规则或WAF规则。

### [!DNL API Mesh for Adobe Developer App Builder] CDN

[!DNL API Mesh]的CDN层终止TLS，以Worker身份运行GraphQL网关，提供全局边缘缓存和自动DDoS/WAF，并将`edge‑graph.adobe.io`/`edge‑sandbox‑graph.adobe.io`公开为公共网状端点；客户可以在前端添加自己的CDN，但[!DNL API Mesh]的CDN由Adobe修复和管理，客户无法配置自己的WAF规则。

有关[!DNL API Mesh]安全功能的详细信息，请参阅[API Mesh文档](https://developer.adobe.com/graphql-mesh-gateway/mesh/security/){target="_blank"}。

### 后端CDN

内置CDN保护[!DNL Adobe Commerce as a Cloud Service]。

由于[!DNL Adobe Commerce as a Cloud Service]架构，当商家在复合单元格（如`na1`、`eu1`、`au1`或其他地理区域）中设置实例时，将公开三个公共表面：

| 表面 | 示例URL模式 |
| --- | --- |
| 管理员UI | `https://<region>.admin.commerce.adobe.com/<tenant-id>/admin/` |
| REST API | `https://<region>.api.commerce.adobe.com/<tenant-id>/<endpoint>` |
| GRAPHQL API | `https://na1.api.commerce.adobe.com/<tenant_id>/graphql/` |

[!DNL Adobe Commerce as a Cloud Service]使用组合的WAF和CDN：

- **WAF** — 所有[!DNL Adobe Commerce as a Cloud Service]公共表面的Web应用程序防火墙保护。
- **CDN** - Edge为静态资源缓存和可缓存的GraphQL响应。

WAF和CDN由[!DNL Adobe Commerce as a Cloud Service]平台管理，客户无法对其进行配置。

### DDoS保护

内置的CDN和WAF提供网络层和HTTP层DDoS保护。 [!DNL Adobe Commerce as a Cloud Service]不会直接向商家公开这些WAF或DDoS日志。

## 数据存储和加密

如果数据存储在[!DNL App Builder]中，则商家可以引用[!DNL App Builder] [存储选项](https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/storage/)。 [!DNL App Builder]强制租户隔离，并且访问这些服务中存储的数据被限制为执行操作的运行时命名空间。 存储中没有数据加密。

使用[!DNL API Mesh]时，密钥应存储在网格配置的`secrets.yaml`文件中。 [!DNL API Mesh]使用AES-256加密([https://developer.adobe.com/graphql-mesh-gateway/mesh/advanced/secrets/](https://developer.adobe.com/graphql-mesh-gateway/mesh/advanced/secrets/))加密这些密钥。

存储在[!DNL Adobe Commerce as a Cloud Service]中的任何数据都使用AES 256位加密进行静态加密，所有数据都使用TLS 1.2或更高版本通过HTTPS进行传输加密。
