---
title: '[!DNL Adobe Commerce Optimizer Connector]'
description: 了解介于 [!DNL Adobe Commerce] 和 [!DNL Adobe Commerce Optimizer]之间的目录同步、搜索和店面投放的 [!DNL Adobe Commerce Optimizer Connector] 。
feature: Integration, Storefront, Configuration
badgePaas: label="仅限PaaS" type="Informative" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于云项目（Adobe管理的PaaS基础架构）和内部部署项目上的Adobe Commerce 。"
autotag-review: '2026-06-09T19:00:00.000Z'
TQID: 'https://experienceleague.adobe.com/-C-XP5YYxwyGrkvVR6CDd-FpDybqnlaKMmFPKOKUbFA'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
  - id: dad884f1-e840-49a1-970e-2f965bdbc410
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 13c9dae2f2f8442f2d5c7be5f6e3317b94956cf0
workflow-type: tm+mt
source-wordcount: 1087
ht-degree: 0%

---

# [!DNL Adobe Commerce Optimizer Connector]

[!DNL Adobe Commerce Optimizer Connector]是[!DNL Adobe Commerce]（云或内部部署）和[!DNL Adobe Commerce Optimizer]之间的本机第一方集成。 它将您的[!DNL Adobe Commerce]存储中的目录和定价数据同步到[!DNL Adobe Commerce Optimizer]中，以便您可以：

- 支持&#x200B;**AI驱动的产品发现和推荐**
- 运行&#x200B;**高性能Headless店面**（包括由[!DNL Edge Delivery Services]提供支持的Commerce店面）
- 在单个位置分析&#x200B;**之前和之后**&#x200B;个KPI和数据同步运行状况

[!DNL Adobe Commerce]保留您的产品、价格和目录结构记录系统。 [!DNL Adobe Commerce Optimizer]成为您的体验和销售层，向任何连接的店面或渠道提供快速的相关结果。

## 主要优势 {#key-benefits}

| 收益 | 这对您意味着什么 |
| --- | --- |
| **没有要生成的自定义连接器** | 使用受支持的第一方集成，而不是编写和维护定制的信息源与脚本。 |
| **使用[!DNL Adobe Commerce Optimizer]**&#x200B;更快实现价值 | 在现有[!DNL Adobe Commerce]部署之上打开AI 搜索、推荐和Headless店面。 |
| **与Commerce范围一致** | 自动将网站、商店视图和客户组映射到[!DNL Adobe Commerce Optimizer]个目录结构（目录源和价格手册）。 |
| **操作可见性** | 从专用[!UICONTROL Data Feed Sync Status]视图中监视信息源运行状况、上次同步时间和每个SKU的状态。 |
| **面向SaaS的未来路径** | 提供从Commerce在云或内部部署到[!DNL Adobe Commerce as a Cloud Service] + [!DNL Adobe Commerce Optimizer]的分阶段迁移路径，无需重新平台。 |

## 连接器架构 {#connector-architecture}

下图说明了连接器的端到端架构，从[!DNL Adobe Commerce]到[!DNL Adobe Commerce Optimizer]再到店面和结帐系统。

![Adobe Commerce Optimizer Connector端到端架构图](./assets/aco-connector-end2end-architecture.png){width="700" zoomable="yes"}

在此架构中：

- [!DNL Adobe Commerce] （在云或本地）是记录和馈送制作系统
- 连接器可导出目录、价格和类别信息源
- [!DNL Adobe Commerce Optimizer]将信息源数据摄取并标准化到目录源、价格手册和目录视图中
- 店面（[!DNL Edge Delivery Services]上的Commerce店面或自定义Headless内部版本）调用[!DNL Adobe Commerce Optimizer]个GraphQL API以进行发现和推荐，并调用[!DNL Adobe Commerce]或其他连接的第三方平台以进行购物车和结账操作

连接器基于[[!DNL SaaS Data Export]](/help/data-export/overview.md)构建，将收集的馈送映射到[!DNL Catalog Data Ingestion API]格式并处理身份验证和提交。 有关同步行为、范围控制和错误处理，请参阅[连接器同步管道](/help/aco-connector/connector-sync-pipeline.md)。

## 连接器如何与[!DNL Adobe Commerce]配合使用 {#how-the-connector-works-with-adobe-commerce}

[!DNL Adobe Commerce Optimizer Connector]通过使用您现有的Commerce范围（网站和商店视图）和客户分段来填充[!DNL Adobe Commerce Optimizer]目录模型来进行操作：

![将Commerce数据映射到Adobe Commerce Optimizer](./assets/storeview-to-catalogview-mapping.png){width="750" zoomable="yes"}

- **存储视图→目录源** — 每个存储视图在[!DNL Adobe Commerce Optimizer]中成为单独的目录Source。 该来源包括本地化的产品属性和任何特定于商店视图的数据
- **网站→价格手册** — 每个[!DNL Adobe Commerce]网站都映射到[!DNL Adobe Commerce Optimizer]中的一个或多个价格手册。 网站定价和客户组定价导出为价格手册和价格条目
- **客户组→价格变体** — [!DNL Adobe Commerce]客户组定价在相关的价格手册中显示为附加条目

[!DNL Adobe Commerce Optimizer]摄取数据后，您可以配置：

- [!DNL Adobe Commerce Optimizer] Studio中的&#x200B;**目录视图和策略**（用于生成区域、品牌或特定于客户的子集）
- **产品发现** （搜索、Facet、促销规则）
- **[!DNL Product Recommendations]**

启用连接器后，[!DNL Adobe Commerce]实例将保留目录和价格数据的记录系统。 当您在[!DNL Adobe Commerce]中更新数据时，连接器会将这些更新同步到[!DNL Adobe Commerce Optimizer]实例。

>[!NOTE]
>
>有关配置[!DNL Adobe Commerce Optimizer]的详细信息，请参阅[[!DNL Adobe Commerce Optimizer] 促销工具](/help/optimizer/overview.md#quick-tour)。

## 典型工作流 {#typical-workflows}

这些工作流描述团队如何设置和使用[!DNL Adobe Commerce Optimizer Connector]。 有关如何设置集成和启用这些工作流的详细信息，请参阅[开始使用](/help/aco-connector/get-started.md)。

### 初始设置和配置 {#initial-setup}

请参阅&#x200B;_开始使用_&#x200B;指南中的[配置步骤](/help/aco-connector/get-started.md#configuration-steps)。

### 正在进行的数据同步 {#ongoing-sync}

初始配置完成后，连接器支持：

- 针对初始迁移或大型结构更改的&#x200B;**完整目录同步**
- 当产品或价格发生变化时，为持续更新进行&#x200B;**增量同步**
- 针对目标馈送重新同步命令&#x200B;**&#x200B;**

有关自动同步行为、cron计划和错误处理，请参阅[连接器同步管道](/help/aco-connector/connector-sync-pipeline.md)。 在完全目录同步或大型更新之前，请使用[估计数据量和同步时间](/help/aco-connector/reference/estimate-data-volume-sync-time.md)来计划时间并避免站点中断。

以下源可用于[!DNL Adobe Commerce Optimizer Connector]：

- `products` — 产品数据
- `productAttributes` — 产品属性的元数据
- `priceBooks` — 价格手册
- `prices` — 产品价格
- `categories` — 类别数据

有关其他详细信息，请参阅以下主题：

- 验证目录数据同步并手动重新同步连接器源： [管理同步](/help/aco-connector/data-sync-manage.md)
- 有关[!DNL Adobe Commerce] CLI重新同步操作，请参阅[使用Commerce CLI同步源](/help/data-export/data-export-cli-commands.md)
- [[!DNL Adobe Commerce Optimizer Connector]模块和馈送端点](/help/aco-connector/reference/connector-reference.md)
- [连接器信息源的字段映射](/help/aco-connector/reference/field-mapping.md)

### 配置推销和店面 {#merchandising-storefronts}

在[!DNL Adobe Commerce Optimizer]中提供[!DNL Adobe Commerce]数据后，请使用[[!DNL Adobe Commerce Optimizer] Studio](/help/optimizer/overview.md#quick-tour)将推销和店面体验连接到您的同步目录。 典型的后续步骤包括：

- **目录视图和策略** — 从[!UICONTROL Store setup]菜单定义区域、品牌或客户特定的子集和访问规则。 要限制可以查询目录视图的人员，请参阅[私有目录视图](/help/optimizer/setup/private-catalog-view.md)
- **产品发现和推荐** — 在[!UICONTROL Merchandising]菜单中配置搜索、Facet、促销规则、同义词和推荐单位。 在[!DNL Adobe Commerce Optimizer]中管理搜索和推荐行为；[!DNL Adobe Commerce]管理员中的[!DNL Live Search]和[!DNL Product Recommendations]设置不再适用于这些流
- **店面连接** — 在正确的[!DNL Adobe Commerce Optimizer]租户、目录视图和促销API端点指向[!DNL Edge Delivery Services]上的Commerce店面或第三方Headless内部版本。 有关自定义Headless集成，请参阅[Headless店面集成](/help/aco-connector/headless-storefront.md)。 有关第三方集成的示例，请参阅针对 [!DNL Adobe Commerce Optimizer][&#128279;](/help/optimizer/developer/salesforce-connector.md)的Salesforce Commerce Connector
- **结帐** — 将购物车、结帐、订单管理和客户帐户保留在[!DNL Adobe Commerce]或连接的第三方平台上。 必要时使用[!DNL App Builder]和[!DNL API Mesh]进行购物车切换

有关分步配置指南，请参阅[开始使用](/help/aco-connector/get-started.md)和[[!DNL Adobe Commerce Optimizer] 促销工具](/help/optimizer/overview.md#quick-tour)。

## 支持的方案 {#supported-scenarios}

连接器专为云和本地部署中具有[!DNL Adobe Commerce]的B2C商家设计，这些商家希望采用[!DNL Adobe Commerce Optimizer]而不重建其后端。

**常见用例：**

- **Storefront迁移到Edge Delivery**
保留您现有的[!DNL Adobe Commerce]后端，将PLP/Search/PDP移动到由[!DNL Adobe Commerce Optimizer]提供支持的[!DNL Edge Delivery Services]店面

- **扩展目录和搜索性能**
将繁重的目录索引和搜索卸载到[!DNL Adobe Commerce Optimizer]的SaaS服务，同时在[!DNL Adobe Commerce]中保留产品和价格所有权

- **增量SaaS采用**
使用连接器作为向[!DNL Adobe Commerce as a Cloud Service] + [!DNL Adobe Commerce Optimizer]迈进的踏板，并具有兼容的可组合[!DNL Adobe Commerce]目录

## 责任和实施先决条件 {#responsibilities-prerequisites}

[!DNL Adobe Commerce]是产品、定价和客户组的真实来源。 在[!DNL Adobe Commerce]中进行更改，然后连接器将它们同步到[!DNL Adobe Commerce Optimizer]。

**[!DNL Adobe Commerce Optimizer]负责：**

- 目录建模（目录来源、价格手册、目录视图、策略）
- 产品发现和推荐
- 店面量度、数据同步功能板和成功量度报表

**连接器不是：**

- 修改[!DNL Adobe Commerce]购物车、结账或订购流程
- 自动配置店面项目（Commerce Storefront / [!DNL Edge Delivery Services]工具句柄）

**开始之前：**

- 验证[!DNL Adobe Commerce]是否满足最低版本和[!DNL Adobe Commerce Optimizer Connector]要求。 有关详细信息，请参阅[开始使用](/help/aco-connector/get-started.md#requirements-to-use-the-integration)。
- 确保您具有IMS组织访问权限、[!DNL Adobe Commerce Optimizer]实例以及必要的凭据和区域详细信息。

>[!MORELIKETHIS]
>
> - [开始使用 [!DNL Adobe Commerce Optimizer Connector]](/help/aco-connector/get-started.md) — 设置集成并启用关键工作流。
> - [连接器同步管道](/help/aco-connector/connector-sync-pipeline.md) — 了解同步机制、初始化和错误处理。
> - [管理同步](/help/aco-connector/data-sync-manage.md) — 验证目录数据同步并手动重新同步馈送。
> - [连接器馈送的字段映射](/help/aco-connector/reference/field-mapping.md) — 查看所有馈送的字段级数据映射。
> - [疑难解答方案](/help/aco-connector/troubleshooting/troubleshooting-scenarios.md) — 解决配置错误或意外的同步结果。
> - [发行说明](/help/aco-connector/release-notes.md) — 查看连接器更新和已知问题。
