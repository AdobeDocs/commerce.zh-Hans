---
title: ' [!DNL Adobe Commerce as a Cloud Service]的可观察性'
description: 了解可用于 [!DNL Adobe Commerce as a Cloud Service]的可观察性工具和遥测功能，包括量度、日志记录和跟踪。
feature: Cloud, Integration
role: Admin, Developer
level: Intermediate
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目（Adobe管理的SaaS基础架构）。"
source-git-commit: 3c10ecdea3d06295013c9c6e2d6869afd750a0b9
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---

# 可观测性

可观察性是操作[!DNL Adobe Commerce as a Cloud Service]的关键方面。 它包括对遥测数据（包括量度、日志记录和跟踪）的收集、处理和可视化，以便您可以监控应用程序运行状况、诊断性能问题并优化Commerce平台及其集成的可靠性。

## [!DNL Adobe Commerce as a Cloud Service]

### 可观察性概述

可观察性使您能够了解Adobe Commerce店面以及所有连接的App Builder应用程序的运行状况和性能。 通过收集整个商业生态系统的遥测数据，您可以：

* **跟踪量度**，如API响应时间、请求和错误率以及资源利用率，以监控实时性能和竞价趋势。
* **将应用程序、基础架构、CDN和集成中的日志**&#x200B;集中到单个视图中，以加快故障排除。
* **跟踪请求**&#x200B;从前端通过Commerce和连接的应用程序进行端到端传输，帮助您在瓶颈和故障影响客户之前查明它们。

这些功能共同帮助您快速识别和解决问题、优化性能并确保为客户提供可靠的体验。 [可观察性概述](https://developer.adobe.com/commerce/extensibility/observability/)说明[!DNL Adobe Commerce as a Cloud Service]如何使用OpenTelemetry在事件、Webhook和App Builder应用程序中统一此遥测收集。

![可观察性体系结构](./assets/observability.png){width="600" zoomable="yes"}

Adobe Commerce通过OpenTelemetry支持以下可观察性工具：

* Elasticsearch
* Grafana
* 耶格
* New Relic
* 普罗米修斯
* Splunk
* 齐普金

### 配置订阅

[在[!UICONTROL Admin]中或通过REST API配置可观察性订阅](https://developer.adobe.com/commerce/extensibility/observability/configuration/)，以将日志、量度或跟踪路由到任何与OpenTelemetry兼容的终结点。 每个订阅都以特定组件为目标（webhook、事件或[!UICONTROL Admin UI SDK]）。

### 可观察性REST API

[可观察性REST API](https://developer.adobe.com/commerce/extensibility/observability/api/)提供以编程方式创建、检索、更新和删除可观察性订阅的端点。 使用这些端点可跨实例自动进行配置。

## Adobe Developer App Builder

### App Builder工具

[在 [!DNL App Builder]](https://developer.adobe.com/commerce/extensibility/observability/app-builder/)中实施可观察性，以将跟踪上下文从Commerce传播到您的[!DNL App Builder]操作中，以使来自两个系统的日志和跟踪在可观察性平台中相互关联。 涵盖基于webhook的集成和基于事件的集成的检测。

[!DNL App Builder]还为[管理应用程序日志](https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/application_logging/logging)提供内置工具，包括CLI和Developer Console访问以及到Splunk、Azure和New Relic等外部解决方案的日志转发。

### 遥测库

[`@adobe/aio-lib-telemetry`](https://github.com/adobe/aio-lib-telemetry/blob/main/docs/usage.md)库是App Builder操作用于发出与OpenTelemetry兼容的日志和跟踪的库。 介绍安装、配置和导出程序设置。

### 本地开发和测试

[在部署之前，在本地测试可观察性设置](https://developer.adobe.com/commerce/extensibility/observability/local-development/)。 使用[!DNL Grafana]进行可视化和隧道转发（例如，[!DNL Ngrok]）以接收来自开发计算机上远程Commerce实例的遥测。

## [!DNL API Mesh]

### API Mesh记录

[API Mesh日志记录](https://developer.adobe.com/graphql-mesh-gateway/mesh/advanced/logging/)允许您使用射线ID监视和调试流经您的网格的请求。 批量导出日志或将日志转发到类似[!DNL New Relic]的平台以进行集中分析。

## 店面

### CDN和实时用户监控

[代理真实用户监控(RUM)](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/content-delivery-network/?lang=zh-Hans#proxy-rum-through-the-origin-to-avoid-a-tls-handshake)通过您的CDN源收集数据，以消除额外的TLS握手并改进前端性能测量。

## 可观察性视频

以下视频概括介绍了[!DNL Adobe Commerce as a Cloud Service]中的可观察性产品：

* [App Builder可观察性视频](https://experienceleague.adobe.com/zh-hans/docs/commerce-learn/tutorials/observability/overview){target="_blank"}
* [API Mesh视频](https://experienceleague.adobe.com/zh-hans/docs/commerce-learn/tutorials/extensibility/api-mesh/getting-started-api-mesh){target="_blank"}
