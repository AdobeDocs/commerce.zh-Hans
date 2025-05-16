---
title: 迁移到 [!DNL Adobe Commerce as a Cloud Service]
description: 了解如何迁移到 [!DNL Adobe Commerce as a Cloud Service]。
exl-id: 9065c92a-f6b2-4464-8ec0-5c549bf78104
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目(Adobe管理的SaaS基础架构)。"
source-git-commit: 34057c1e55ff117ea7aab4407f31548ce826691b
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 0%

---

# 迁移到[!DNL Adobe Commerce as a Cloud Service]

{{accs-early-access}}

[!DNL Adobe Commerce as a Cloud Service]提供大部分现成的配置。 但是，如果您要从Cloud上的现有Adobe Commerce或内部部署实例进行迁移，则需要根据特定配置执行不同的迁移操作。

## 迁移路径

[!DNL Adobe Commerce as a Cloud Service]支持多个迁移路径，具体取决于您的时间线、店面和自定义设置。

作为完整迁移的替代方法，[!DNL Adobe Commerce as a Cloud Service]支持使用Commerce Optimizer或增量方法执行分阶段迁移。

* **增量迁移** — 此方法涉及分阶段迁移您的数据、自定义项和集成。 这种方法非常适用于具有许多自定义项的大型商家，这些商家希望按照自己的步调将其复杂的自定义项和数据逐步过渡到[!DNL Adobe Commerce as a Cloud Service]。

![增量迁移](./assets/incremental.png){width="600" zoomable="yes"}

* **Commerce Optimizer** — 此方法允许您循环迁移，方法是使用Commerce Optimizer作为过渡阶段，按照自己的步调将复杂的自定义项和数据移动到[!DNL Adobe Commerce as a Cloud Service]。 Commerce Optimizer提供对由目录渠道和策略提供支持的促销服务、由Edge Delivery提供支持的Commerce店面以及由AEM Assets提供支持的产品可视化图表的访问权限。

![迭代迁移](./assets/optimizer.png){width="600" zoomable="yes"}

* **完全迁移** — 此方法包括同时迁移所有数据、自定义项和集成。 这种方法非常适用于那些自定义项很少且想要快速过渡到[!DNL Adobe Commerce as a Cloud Service]的小型商家。

下表概述了不同存储前端和配置的迁移过程：

|                    | LUMA店面 | PWA店面 | 由Edge Delivery提供支持的Commerce店面 | Headless |
|--------------------|----------------------------------------|----------------------------------------|------------------------------------------------------|----------------------------------------|
| 数据迁移 | 必填 | 必填 | 必填 | 必填 |
| 店面 | 迁移到由Edge Delivery提供支持的Commerce Storefront | 迁移到由Edge Delivery提供支持的Commerce Storefront或维护 | 无影响 | 无影响 |
| API网格 | 生成新网格 | 生成新网格或重新配置现有网格 | 生成新网格或重新配置现有网格 | 生成新网格或重新配置现有网格 |
| 集成 | 利用集成入门工具包 | 利用集成入门工具包 | 利用集成入门工具包 | 利用集成入门工具包 |
| 自定义 | 移动到App Builder和API Mesh | 移动到App Builder和API Mesh | 移动到App Builder和API Mesh | 移动到App Builder和API Mesh |
| Assets管理 | 使用OOTB时需要迁移 | 使用OOTB时需要迁移 | 使用OOTB时需要迁移 | 使用OOTB时需要迁移 |
| 扩展 | 迁移到App Builder | 迁移到App Builder | 迁移到App Builder | 迁移到App Builder |

如表所示，每次迁移的缓解措施将包括：

* **数据迁移** — 使用提供的迁移工具将数据从现有实例迁移到[!DNL Adobe Commerce as a Cloud Service]。
* **店面** — 现有EDS和Headless店面不需要减轻，但LUMA店面需要迁移到由Edge Delivery提供支持的Commerce店面。 PWA Studio店面可以迁移到由Edge Delivery提供支持的Commerce店面，也可以保持其当前状态。 Adobe将提供加速器以帮助店面迁移。
* **[API网格](https://developer.adobe.com/graphql-mesh-gateway)** — 创建新网格或修改现有网格。 Adobe将提供预配置的网格以帮助完成此过程。
* **集成** — 所有集成都需要利用[集成入门工具包](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/)或[[!DNL Adobe Commerce as a Cloud Service] REST API](https://developer.adobe.com/commerce/services/reference/cloud-service/core-admin/)。
* **自定义项** — 所有自定义项都必须移至App Builder和API网格。
* **Assets管理** — 所有资源管理都需要迁移。 如果您已在使用AEM Assets，则无需迁移。
* **扩展** — 任何进程内扩展都需要重新创建为进程外扩展。 到2025年底，Adobe将提供对我们最受欢迎的扩展的访问，以最大程度地缩短构建时间。

## 迁移阶段

从当前Adobe Commerce实例迁移到新[!DNL Adobe Commerce as a Cloud Service]实例主要涉及以下阶段：

* **[准备就绪](#readiness-phase)** — 首先确定您的部署是否已准备好迁移至ACCS。 在此阶段，您还应熟悉ACCS引入的更改&#x200B;。
* **[实施](#implementation-phase)** — 接下来，准备迁移您的代码、店面、扩展和集成。 为了简化过渡，Adobe允许使用[短期和长期迭代方法](#migration-paths)&#x200B;。
* **[上线](#go-live-phase)** — 测试并确认一切都已就绪，然后执行数据迁移。
* **[上线后](#post-go-live-phase)** — 与Adobe合作，在迁移完成后根据需要监视问题并改进性能。

### 就绪阶段

1. 首先查看[!DNL Adobe Commerce as a Cloud Service]体系结构、可扩展性框架和店面功能：

   * [Cloud Services架构上的Adobe Commerce](./overview.md) — 查看平台架构以及它与当前Adobe Commerce实例的差异。
   * [Adobe Commerce可扩展性框架](https://developer.adobe.com/commerce/extensibility/) — 确定您要如何转换当前的自定义设置。
   * [由Edge Delivery提供支持的Commerce店面](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=zh-Hans) — 查看推荐的店面解决方案。

1. 审核您的自定义兼容性：

   * 识别您当前的自定义模块和第三方集成。
   * 使用App Builder评估需要重新实施的自定义项。
   * 将当前自定义项映射到其App Builder扩展等效项。

1. 确认您的店面要求，并确保这些要求与Adobe Edge交付功能保持一致。

1. 检查您当前的第三方集成，并确认API与[!DNL Adobe Commerce as a Cloud Service]平台的兼容性。

### 实施阶段

以下步骤概述了迁移的开发和执行过程：

1. 在[Commerce Cloud Manager](./getting-started.md#create-an-instance)中创建新的[!DNL Adobe Commerce as a Cloud Service]实例。

1. 安装所需的应用和自定义项。 [!DNL Adobe Commerce as a Cloud Service]有权访问我们最受欢迎的应用。 如果您需要其他应用程序或自定义项，可以使用App Builder重新实施它们。

1. 设置以下基于GraphQL的店面之一：

   * [创建Commerce店面](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/?lang=zh-Hans)
   * [使用PWA Studio创建基于GraphQL的自定义店面](https://developer.adobe.com/commerce/pwa-studio/)

1. 将您的数据从以前的Commerce实例迁移到ACCS：

   * 使用数据迁移工具迁移本机Adobe Commerce数据。
   * 迁移第三方扩展和自定义项
   * 迁移配置和集成数据：
      * 使用[Adobe Commerce Integration Starter Kit](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/)传输API Mesh配置、第三方服务和系统集成。

### 上线阶段

在启动之前，请使用沙盒环境验证并测试您的新[!DNL Adobe Commerce as a Cloud Service]实例：

* **功能测试** — 确保迁移的数据、店面功能和自定义无缝工作。

* **性能测试** — 评估存储的速度和可扩展性以确保全局最佳性能。

* **安全审核** — 审查安全措施，包括API访问控制和任何潜在漏洞。

在验证和测试新的[!DNL Adobe Commerce as a Cloud Service]沙盒实例后，即可启动生产实例。

### 上线后阶段

上线后，请执行以下启动后活动：

1. 上线跟进

   * 将流量重定向到新平台并监控性能。
   * 禁用您的旧Adobe Commerce实例。

1. 启动后监测

   * 使用监控工具确保稳定运行并解决任何启动后问题。
