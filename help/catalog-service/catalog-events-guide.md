---
title: Catalog和Adobe I/O Events集成指南
description: 了解如何验证目录数据、为Adobe Commerce配置 [!DNL Adobe I/O Events] 、订阅目录事件类型以及验证使用者的交付。
level: Intermediate
recommendations: noCatalog
role: Admin, Developer
feature: Services, Catalog Service
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c32adafa-ed01-4b31-997e-2413013911b0
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: d8e9d612392967d19d0da56e81337362f9006c2c
workflow-type: tm+mt
source-wordcount: 1566
ht-degree: 0%

---

# 目录事件和[!DNL Adobe I/O Events]集成指南

目录事件是计算机生成的通知，用于描述通过[!DNL Catalog Service]提供的支持的目录更改。 它们支持事件驱动的工作流，例如：

* 使外部缓存或服务与目录更新保持同步。
* 当产品、变体、价格或类别发生更改时触发下游流程。
* 为需要近乎实时的目录更新的Experience Edge和[!DNL Edge Delivery Services]用例提供支持。

有关从[!DNL Adobe Commerce]到您的事件使用者的端到端路径，请参阅[通过 [!DNL Adobe I/O Events]](#event-delivery-through-adobe-io-events)的事件传递。

## 支持的事件类型 {#supported-event-types}

目录活动侧重于通过[!DNL Adobe Developer Console]公开的店面相关更改。 当前支持以下订阅。

| 订阅 | 活动 |
| --- | --- |
| 产品更新 | 通过[!DNL Catalog Service]提供的产品的产品创建、更新和删除更改 |
| 价格更新 | 价格创建、更新和删除影响店面目录数据的更改 |

每个事件包括：

* 描述变更类型的事件标识符。
* 实体和环境上下文，例如实例ID和SKU。
* 描述已更改实体和相关作用域信息的有效负载。


## 示例事件负载

**ProductUpdated事件**

```json
{
  "imsOrgId": "aaa-0",
  "instanceId": "instance-9",
  "eventCode": "productUpdated",
  "sku": "1234",
  "links": [
    {"type":  "variantOf", "sku": "5678"}
   ],
  "scope": [
    { "storeViewCode": "US-us" },
    { "storeViewCode": "FR-fr" },
    { "storeViewCode": "DE-de" }
  ]
}
```

**PriceUpdated事件**

```json
{
  "imsOrgId": "aaa-0",
  "instanceId": "instance-9",
  "eventCode": "priceUpdated",
  "sku": "1234",
  "scope": [
    {
      "websiteCode": "website1",
      "customerGroupCode": "customer-group-code1"
    },
    {
      "websiteCode": "website2",
      "customerGroupCode": "customer-group-code2"
    }
  ]
}
```

## 通过[!DNL Adobe I/O Events]的事件传递 {#event-delivery-through-adobe-io-events}

[!DNL Adobe I/O Events]将目录事件交付给您的集成。 下图显示了从[!DNL Adobe Commerce]到[!DNL Catalog Service]和[!DNL Adobe I/O Events]的目录更改到订阅使用者的高级流程：

![从Adobe Commerce通过目录服务和Adobe I/O Events到订阅用户的目录事件高级流](assets/catalog-service-event-pipeline.png)

以下步骤更详细地解释了每次切换：

1. **Adobe Commerce →目录服务**

[!DNL Adobe Commerce]使用支持的SaaS Data Export扩展将目录数据导出到[!DNL Catalog Service]。

1. **目录服务正在处理**

   * [!DNL Catalog Service]进程支持的目录更改，并为事件交付准备这些更改。

1. →的&#x200B;**目录服务**

* 目录事件已发布到[!DNL Adobe I/O Events]。
* 使用者使用日记、Webhook、[!DNL Adobe I/O Runtime]、Amazon EventBridge或其他支持的投放机制进行订阅。

[!DNL Adobe I/O Events]提供：

* *每个订阅者至少投放*&#x200B;一次（可能存在重复事件）。
* 不保证跨投放订购。

您的消费者必须处理重复的事件和乱序投放。 有关实施指南，请参阅[幂等性](#idempotency)。

## 用例 {#use-cases}

您可以在多个方案中使用目录事件。

### 静态站点和边缘交付

* 当目录数据更改时，重新生成目录页面和店面片段或使其失效。
* 避免频繁轮询[!DNL Catalog Service] API。

### 搜索索引和缓存

* 触发下游搜索索引中的增量更新。
* 当产品或类别数据更改时，更新缓存层或目录的外部视图。

### 与外部系统集成

* 将目录更改转发给外部系统，如PIM、定价引擎或其他业务线系统。
* 保持下游应用程序同步，而无需直接访问数据库。

### 监控和可观察性

将目录事件与现有的监视（例如，[!DNL Grafana]和[!DNL Prometheus]）合并为：

* 监视事件吞吐量。
* 检测目录更新卷中的异常。

## 启用目录事件 {#enable-catalog-events}

要启用端到端目录事件，请执行以下步骤。

>[!PREREQUISITES]
>
>在启用目录事件之前，请确保您具有以下各项：
>
>* 已启用[!DNL Catalog Service]的受支持Adobe Commerce环境。
>* [已为Adobe Commerce](https://developer.adobe.com/commerce/extensibility/events/configure-commerce)配置 [!DNL Adobe I/O] 连接。
>* 在配置了Commerce环境的同一IMS组织中访问[!DNL Adobe Developer Console]。
>* 若要验证是否同步到Commerce SaaS服务，请在“管理员”中使用&#x200B;**[!UICONTROL Data Management Dashboard]**。
>* 仪表板验证需要产品推荐v6.0、[!DNL Live Search] v4.1.0+或[!DNL Catalog Service] v1.17+。 Adobe建议将您的Commerce项目更新到这些服务的最新支持版本。 对于较早的服务版本，请使用[目录同步](https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/data-services/catalog-sync)进行同步验证。


>[!NOTE]
>
>要使用目录事件，请首先为[!DNL Adobe I/O Events]配置Commerce环境，然后在[!DNL Adobe Developer Console]中注册事件订阅。
>
>如果配置后您的环境未出现在[!DNL Adobe Developer Console]中，请验证您是否登录到正确的IMS组织，以及您的帐户是否具有所需的访问权限。 如果环境仍未显示，请联系Adobe支持部门。

### 验证目录数据 {#verify-catalog-data}

在配置之前，请验证[!DNL Catalog Service]是否具有来自您的[!DNL Commerce]实例的当前目录数据。 目录事件取决于[!DNL SaaS Data Export]完成两个阶段 — 确认&#x200B;**两者**：

1. 确认从Commerce **成功导出**&#x200B;信息源。

   从[!DNL Adobe Commerce]管理员中，打开[数据馈送同步状态](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status)页面(**[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**)，并确认每个[!DNL Catalog Service]馈送的上次导出状态都成功。

1. 确认从[!DNL Adobe Commerce]管理员成功&#x200B;**同步到连接的Commerce服务**。

   从[!DNL Adobe Commerce]管理员中，打开[数据管理功能板](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard) (**[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Management Dashboard]**)，并验证同步的产品数据是否包含预期的产品。

### 注册并订阅[!DNL Adobe I/O Events] {#register-events}

定义要订阅的Commerce事件，然后在项目中注册它们。

如果您的实例不在选择列表中，则它未连接到[!DNL Adobe I/O]。 有关解决问题的说明，请参阅&#x200B;*Adobe Commerce Developer*&#x200B;文档中的[配置 [!DNL Adobe I/O] 连接](https://developer.adobe.com/commerce/extensibility/events/configure-commerce#configure-the-adobe-io-connection)。

1. 从[!DNL Adobe Developer Console]，登录到用于Commerce项目的同一IMS组织。

1. 为Commerce目录事件创建项目，或将事件API添加到现有项目。

   * 在顶部导航中选择&#x200B;**[!UICONTROL APIs and services]**。

   * 在&#x200B;**[!UICONTROL Browse APIs and services]**&#x200B;页面上，选择&#x200B;**[!UICONTROL Events]**&#x200B;选项卡。

   * 快速查找Commerce Catalog Events API。 在搜索框中键入&#x200B;_Catalog_，或按&#x200B;**[!UICONTROL Commerce]**&#x200B;产品筛选。

   * 在&#x200B;**[!UICONTROL Commerce Catalog Events]**&#x200B;信息卡上，选择&#x200B;**[!UICONTROL Project]**。

   在Browse API和服务页上选择了![Commerce目录事件提供程序](assets/catalog-event-select-provider.png){width="600" zoomable="yes"}

1. 配置事件注册。

   选择要从中接收事件通知的Commerce实例。 然后选择&#x200B;**[!UICONTROL Next]**。

   在事件注册屏幕上选择![Commerce实例](assets/catalog-event-registration.png){width="600" zoomable="yes"}

1. 选择要订阅的事件。

   选择要接收的支持事件订阅，如&#x200B;**[!UICONTROL Product Update]**&#x200B;或&#x200B;**[!UICONTROL Price Update]**。 然后选择&#x200B;**[!UICONTROL Next]**。

   在注册屏幕上选择订阅的![事件类别](assets/catalog-event-subscription.png){width="600" zoomable="yes"}

1. 添加OAuth服务器到服务器凭据。

   输入&#x200B;**[!UICONTROL Credential name]**。 然后选择&#x200B;**[!UICONTROL Next]**。

1. 输入&#x200B;**[!UICONTROL Event registration name]**&#x200B;和&#x200B;**[!UICONTROL Event registration description]**。 然后选择&#x200B;**[!UICONTROL Next]**。

1. 在最终注册屏幕上，接受默认消费者Journaling API 。

   通过默认的Journaling API使用者，您可以测试事件注册并确认事件已交付。 如果您已配置webhook或[!DNL Adobe I/O Runtime]操作使用者，请在此处选择它。 否则，请在消费者准备就绪后编辑事件注册。

   ![在事件注册完成屏幕上选择的日记API使用者默认值](assets/catalog-event-consumer.png){width="600" zoomable="yes"}

1. 选择&#x200B;**[!UICONTROL Complete registration]**。

### 配置事件消费者 {#configure-consumer}

1. 配置使用者，例如：

   * webhook端点
   * [!DNL Adobe I/O Runtime]操作
   * 另一个受支持的目标

1. 如果在注册期间未选择消费者，请编辑事件注册以添加消费者详细信息。

   * 从[!DNL Adobe Developer Console]中，编辑您的项目。 然后，选择您创建的事件注册。

   * 在事件注册详细信息页面上，选择&#x200B;**[!UICONTROL Edit Events Registration]**。

   * 选择&#x200B;**[!UICONTROL Next]**，直到到达消费者选择屏幕。 然后，选择您配置的消费者。

   * 将消费者更新到您配置的目标。 然后选择&#x200B;**[!UICONTROL Save configured events]**。

### 验证事件流 {#validate-event-flow}

为您的环境启用了目录事件。 当[!DNL Commerce]中的目录数据发生更改时，更新将通过[!DNL Catalog Service]流向[!DNL Adobe I/O Events]，并且您订阅的使用者将收到相应的目录事件。 在生成生产集成之前，请查看[限制和最佳实践](#limits-and-best-practices)。
1. 进行简单的受支持目录更改，如更新产品名称或更改价格。

1. 确认以下结果：

   * 更改通过[!DNL Catalog Service] API可见。
   * 您的[!DNL Adobe I/O Events]消费者会收到相应的产品或价格事件。


## 限制和最佳实践 {#limits-and-best-practices}

在构建目录事件时，请遵循这些最佳实践。

### 幂等性 {#idempotency}

[!DNL Adobe I/O Events]可以多次交付相同的目录事件，单个产品的事件可能会不按顺序到达。 通过以下方式设计幂等消费者：

* 将实体ID与版本或时间戳字段一起使用。
* 安全地忽略相同更改的重复通知。

### 吞吐量和背压

更新率高的大型目录可能会产生大量的事件量。 确保：

* 使用者可以在吞吐量高峰时处理事件。
* 您可以根据需要使用缓冲、批量处理或队列。

### 安全性和隔离

* [!DNL Adobe I/O Events]强制实施&#x200B;*租户隔离*。
* 您的组织仅接收其自身环境和权利的事件。

### 模式演变

目录事件负载遵循与[!DNL Catalog Service] API相同的概念模型。 要保持向前兼容，请执行以下操作：

* 尽可能避免严格执行模式。
* 忽略未知字段而非失败。

## 目录事件疑难解答 {#troubleshoot-catalog-events}

如果目录事件缺失或延迟，请完成这些步骤。

1. **检查目录服务数据**

   [使用 [!DNL Catalog Service] API](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/)确认已成功存储目录更改。

1. **验证[!DNL SaaS Data Export]**

   目录事件需要[!DNL Catalog Service]中的当前数据。 确认导出路径的两个阶段：

   * 从Commerce导出&#x200B;**信息源** — 在[数据信息源同步状态](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status)页面或`var/log/saas-export.log`中，确认已成功从[!DNL Commerce]导出[!DNL Catalog Service]信息源。

   * **同步到连接的Commerce SaaS服务** — 在[数据管理功能板](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)、[目录同步](https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/data-services/catalog-sync)或导出日志中，确认数据已成功同步到[!DNL Catalog Service]。

   有关导出和同步作业的疑难解答，请参阅[将数据与SaaS数据导出同步](../data-export/data-sync-manage.md)和[日志记录和疑难解答](../data-export/troubleshooting/logging.md)。

1. **验证[!DNL Adobe I/O Events]配置**

   确认：

   * 您已在[!DNL Adobe Developer Console]中登录到正确的IMS组织。
   * **[!UICONTROL Commerce Catalog Events]**&#x200B;提供程序已启用。
   * 预期的&#x200B;**[!UICONTROL Commerce Catalog Events]**&#x200B;提供程序和环境可见。
   * 订阅处于活动状态。
   * 您的端点、操作或日志使用者可以接收和处理测试事件。

1. **联系Adobe支持**

   打开支持票证时，请选择与&#x200B;**Adobe Commerce应用程序**&#x200B;对应的问题原因，并包含以下信息：

   * 目录服务详细信息（环境、区域）。
   * [!DNL Adobe I/O Events]订阅详细信息。
   * 缺失事件的近似时间和描述。

   有关其他帮助，请参阅[支持票证](https://experienceleague.adobe.com/zh-hans/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#support-case)。

>[!MORELIKETHIS]
>
>
>* [登录和安装](installation.md)
>* [开始使用目录服务](get-started.md)
>* [将数据与SaaS数据导出同步](../data-export/data-sync-manage.md)
>* [使用GraphQL API检索目录数据](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/){target="_blank"}
>* [[!DNL Catalog Service] 和API网格](mesh.md)
>* [配置 [!DNL Adobe I/O] 连接](https://developer.adobe.com/commerce/extensibility/events/configure-commerce#configure-the-adobe-io-connection){target="_blank"}
>* [[!DNL Adobe I/O Events]](https://developer.adobe.com/events/docs/guides/){target="_blank"}
