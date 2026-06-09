---
title: Adobe Commerce Optimizer连接器
description: 了解如何将Commerce云或内部部署项目中的数据连接到Adobe Commerce Optimizer
feature: Personalization, Integration, Configuration
badgePaas: label="仅限PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于云项目（Adobe管理的PaaS基础架构）和内部部署项目上的Adobe Commerce 。"
TQID: https://experienceleague.adobe.com/-C-XP5YYxwyGrkvVR6CDd-FpDybqnlaKMmFPKOKUbFA
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: b954ce1acf338978acad4fbb2ec5e01db174bbf9
workflow-type: tm+mt
source-wordcount: 1167
ht-degree: 0%

---

# Adobe Commerce Optimizer连接器

Adobe Commerce Optimizer Connector是Adobe Commerce（云或内部部署）与Adobe Commerce Optimizer之间的原生第一方集成。 它将Adobe Commerce存储中的目录和定价数据同步到Commerce Optimizer中，以使您可以：

- 支持&#x200B;**AI驱动的产品发现和推荐**
- 运行&#x200B;**高性能Headless店面**（包括由Edge Delivery提供支持的Commerce店面）
- 在单个位置分析&#x200B;**之前和之后**&#x200B;个KPI和数据同步运行状况

Commerce保留您的产品、价格和目录结构记录系统。 Commerce Optimizer成为您的体验和营销层，可以为任何连接的店面或渠道提供快速的相关结果。

## 主要优势 {#key-benefits}

| 收益 | 这对您意味着什么 |
| --- | --- |
| **没有要生成的自定义连接器** | 使用受支持的第一方集成，而不是编写和维护定制的信息源与脚本。 |
| 使用Commerce Optimizer **更快的价值实现** | 在现有Adobe Commerce部署之上打开AI 搜索、推荐和Headless店面。 |
| **与Commerce范围一致** | 自动将网站、商店视图和客户组映射到Commerce Optimizer目录结构（目录源和价格手册）中。 |
| **操作可见性** | 从专用数据馈送同步状态视图中监控馈送运行状况、上次同步时间和按SKU显示的状态。 |
| **面向SaaS的未来路径** | 提供了一种从PaaS到Adobe Commerce as a Cloud Service + Optimizer的低风险现代化途径，而无需重新平台。 |

## 连接器架构 {#connector-architecture}

下图说明了连接器的端到端架构，从Adobe Commerce到Commerce Optimizer，再到店面和结账系统。

![Adobe Commerce Optimizer Connector端到端架构图](./assets/aco-connector-end2end-architecture.png){width="700" zoomable="yes"}

在此架构中：

- Adobe Commerce（云或本地）是记录和馈送制作系统
- 连接器导出目录、价格和类别信息源
- Commerce Optimizer摄取信息源数据并将其标准化到目录源、价格手册和目录视图中
- 店面（Edge Delivery上的Commerce店面或自定义Headless内部版本）调用Commerce Optimizer GraphQL API进行发现和建议，并调用Commerce或其他连接的第三方平台进行购物车和结账操作

## 连接器如何使用Adobe Commerce

Adobe Commerce Optimizer Connector通过使用您现有的Commerce范围（网站和商店视图）和客户分段来填充Commerce Optimizer目录模型来进行操作：

![将Commerce数据映射到Adobe Commerce Optimizer](/help/aco-connector/assets/storeview-to-catalogview-mapping.png){width="750" zoomable="yes"}

- **将视图存储→目录源** — 每个存储视图在Commerce Optimizer中都成为单独的目录Source。 该来源包括本地化的产品属性和任何特定于商店视图的数据
- **网站→价格手册** — 每个Commerce网站都映射到Commerce Optimizer中的一个或多个价格手册。 网站定价和客户组定价导出为价格手册和价格条目
- **客户组→价格变体** — Commerce客户组定价在相关的价格手册中显示为附加条目

Commerce Optimizer摄取数据后，您可以配置：

- Commerce Optimizer中的&#x200B;**目录视图和策略**（用于构建区域、品牌或特定于客户的子集）
- **产品发现** （搜索、Facet、促销规则）
- **产品推荐**

启用连接器后，Adobe Commerce实例将保留目录和价格数据的记录系统。 在Commerce中更新数据时，连接器会将这些更新同步到[!DNL Adobe Commerce Optimizer]实例。

>[!NOTE]
>
>有关配置Commerce Optimizer的详细信息，请参阅[[!DNL Adobe Commerce Optimizer] 促销工具](../optimizer/overview.md#quick-tour)。

## 典型工作流 {#typical-workflows}

这些工作流描述团队如何设置和使用Adobe Commerce Optimizer Connector。 有关如何设置集成和启用这些工作流的详细信息，请参阅[开始使用](get-started.md)。

### 初始设置和配置 {#initial-setup}


设置和配置的高层步骤：

1. 安装适用于Adobe Commerce的连接器软件包。

1. 配置身份验证和环境详细信息。

1. 将Commerce范围映射到Commerce Optimizer。

1. 检验连通性。

有关详细说明，请参阅&#x200B;_开始使用_&#x200B;指南中的[配置步骤](./get-started.md#configuration-steps)。

### 正在进行的数据同步 {#ongoing-sync}

初始配置完成后，连接器支持：

- 针对初始迁移或大型结构更改的&#x200B;**完整目录同步**
- 当产品或价格发生变化时，为持续更新进行&#x200B;**增量同步**
- 针对目标馈送重新同步命令&#x200B;**&#x200B;**

Adobe Commerce Optimizer Connector提供以下源：

- `products` — 产品数据
- `productAttributes` — 产品属性的元数据
- `priceBooks` — 价格手册
- `prices` — 产品价格
- `categories` — 类别数据
有关使用Commerce命令行界面(CLI)进行重新同步操作的详细信息，请参阅[CLI resync命令](../data-export/data-export-cli-commands.md#sync-using-cli-commands){target="blank"}。

### 配置推销和店面 {#merchandising-storefronts}

在Commerce Optimizer中提供Commerce数据后，使用Commerce Optimizer Studio将推销和店面体验连接到您的同步目录。

**要配置商品推销和店面：**

1. 在Commerce Optimizer Studio中&#x200B;**创建目录视图和策略**：

   - 按品牌、地区、客户区段或渠道过滤目录
   - 针对每个店面或合作伙伴强制执行数据访问规则

1. 在优化器UI中&#x200B;**配置产品发现和推荐**：

   - 创建促销规则、彩块化、同义词和推荐单位
   - 连接器将所有搜索和推荐配置卸载到Commerce Optimizer（Commerce管理员中的实时搜索规则和产品推荐不再适用于这些流程）

1. **将店面**&#x200B;连接到Commerce Optimizer：

   - 对于由Edge Delivery Services提供支持的Commerce店面，请将店面配置为使用正确的Optimizer租户和目录视图，并通过促销API调用搜索和推荐端点
   - 对于第三方店面，使用Optimizer公共API或SDK进行搜索和推荐调用

   >[!NOTE]
   >
   >有关第三方集成的示例，请参阅适用于Commerce Optimizer的[Salesforce Commerce Connector](../optimizer/developer/salesforce-connector.md)。

1. **在您的现有平台上维护签出**：

   - 在Adobe Commerce或第三方平台中保留购物车、结账、订单管理和客户帐户
   - 与外部结帐系统集成时，使用App Builder和API Mesh进行购物车切换

## 支持的方案 {#supported-scenarios}

该连接器专为具有Adobe Commerce云和内部部署的B2C商家设计，这些商家希望采用Commerce Optimizer而不重建其后端。

**常见用例：**

- **仅更新店面**
保留您现有的Commerce后端，将PLP/Search/PDP移动到由Commerce Optimizer提供支持的Edge Delivery店面

- **扩展目录和搜索性能**
将繁重的目录索引和搜索卸载到Commerce Optimizer的SaaS服务，同时在Commerce中保留产品和价格所有权

- **增量SaaS采用**
使用连接器作为迈向Adobe Commerce as a Cloud Service + Optimizer的垫脚石，并提供兼容的可组合Commerce目录

## 责任和实施先决条件 {#responsibilities-prerequisites}

Commerce是产品、定价和客户组的真实来源。 在Commerce中进行更改；连接器会将这些更改同步到Commerce Optimizer。

**Commerce Optimizer负责：**

- 目录建模（目录来源、价格手册、目录视图、策略）
- 产品发现和推荐
- 店面量度、数据同步功能板和成功量度报表

**连接器不是：**

- 修改Commerce购物车、结账或订购流程
- 自动配置店面项目（Commerce Storefront/Edge Delivery工具处理）

**开始之前：**

- 验证Commerce是否符合最低版本和服务连接器要求。 有关详细信息，请参阅[开始使用](get-started.md#prerequisites)。
- 确保您具有IMS组织访问权限、[!DNL Adobe Commerce Optimizer]实例以及必要的凭据和区域详细信息。

## 相关文档 {#related-documentation}

- 设置集成并启用关键工作流：[Adobe Commerce Optimizer Connector入门](get-started.md)
- 了解Commerce Optimizer概念和架构： [什么是Adobe Commerce Optimizer？](../optimizer/overview.md)
