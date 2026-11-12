---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 0%
---
<!--This shared include file contains the conceptual and architecture overview of catalog views for Adobe Merchandising Services-->

目录视图定义客户端可以检索的产品和定价。 它结合了目录源、目录层、策略和价格手册以支持不同的品牌、地区、业务部门或渠道。

## 什么是目录视图？

目录视图定义产品目录的组织和显示方式。 它们充当过滤器，用于确定：

- 根据业务结构（品牌、地区、经销商）**哪些产品可见**
- **通过链接的价格手册显示什么定价**
- **如何使用策略（品牌、模型、类别等属性）过滤产品**
- **使用什么[目录源](/help/optimizer/setup/catalog-sources.md)**&#x200B;基于区域设置等属性
- **谁可以通过[目录保护](private-catalog-view.md)和[受限访问密钥](restricted-access-keys.md)访问视图的数据**

例如，您可以为以下对象创建单独的目录视图：

- 品牌或业务部门
- 地理区域
- 经销商或合作伙伴渠道
- 具有特定定价的客户区段

## 架构概述

目录视图是Adobe Merchandising服务框架的一部分，该框架将Adobe Commerce基础中使用的网站、商店、商店审核框架替换为更灵活的模型：

![[!DNL Merchandising Services]架构](/help/assets/ccdm-shared/setup/merchandising-svcs-architecture.png)

### 工作原理

**1. 数据摄取**
来自Adobe Commerce后端或其他第三方后端（例如，PIM或ERP）和其他系统的目录数据将摄取到Adobe Merchandising Services数据层中。 每个SKU都包含映射到目录视图、策略和区域设置的区域设置信息和产品属性。 数据获取过程依赖于源系统和集成方法：

- **Adobe Commerce后端** — 系统将导出Commerce目录馈送，将它们映射到数据摄取REST API所需的格式，并将馈送数据同步到Adobe Merchandising Services数据层。 在此模型中，Adobe Commerce管理初始同步和后续更新。 信息源包括产品、类别、产品属性、价格和价格手册。

- **第三方后端或源系统** — 连接器或集成服务通过API、事件或导出馈送从源检索目录数据，然后针对可组合目录数据模型(CCDM)架构映射和验证该数据，并使用数据摄取REST API将数据同步到Adobe Merchandising服务层。 该集成负责初始加载并发送以后的更改。 平台特定的连接器（如Adobe的[Salesforce Commerce Connector](https://experienceleague.adobe.com/zh-hans/docs/commerce/optimizer/developer/salesforce-connector)）可以提供起点。

**2. 统一的基本目录**
引入的数据在目录服务数据管道中创建统一的基本目录。 此单一来源可消除跨业务部门的数据重复。

**3. 目录视图**
多个目录视图代表不同的业务单位（例如，“Texas Retail”、“Texas Retail Secondural”）。 可以在目录视图之间共享区域设置、策略和价格手册，以实现灵活性。

**4. 多渠道交付**
过滤的目录数据会交付到Edge Delivery Services、市场、广告平台和自定义微店面等目标。 有关目录数据投放的详细信息，请参阅[开发人员文档](https://developer.adobe.com/commerce/services/optimizer/)。

当目录视图启用了&#x200B;**[!UICONTROL Catalog Protection]**&#x200B;时，向该目标的投放需要分配的[受限访问密钥](restricted-access-keys.md)中的有效签名令牌；未授权的请求将被拒绝而不是接收目录数据。

### 关键组件

| 组件 | 用途 | 示例 |
|---|---|---|
| **目录视图** | 业务单位或分发渠道 | 经销商网络、地区商店 |
| **策略** | 基于属性的产品过滤器 | 品牌、型号、类别 |
| **区域设置** | 语言/区域设置 | en-US、fr-CA、es-MX |
| **价格手册** | 定价结构 | 零售、批发、员工 |
| **受限访问密钥** | 用于阻止访问受保护目录视图的签名令牌凭据 | 合作伙伴门户密钥、B2B定价密钥 |

### 数据流

1. **摄取** — 从Adobe Commerce后端摄取目录数据
2. **进程** — 应用目录视图、策略和定价
3. **交付** — 将过滤的目录提供给店面、市场等

## 主要功能

| 功能 | 收益 |
|---|---|
| **单基目录** | 消除跨业务部门的重复数据 |
| **灵活的定价** | 针对不同客户区段，每个SKU有多个价格手册 |
| **可缩放** | 高效地管理2亿多个SKU |
| **多渠道** | 将目录提供给店面、市场和广告平台 |
| **实时更新** | 快速更新促销和营销活动的目录数据 |
| **专用目录视图** | 使用签名令牌验证将目录视图限制为授权客户端 |

## 用例

### 多品牌企业集团

**挑战**：管理多个品牌、国家和语言<br>
**解决方案**：每个品牌/区域组合只有一个目录，其中具有目录视图

### 汽车零部件经销商

**挑战**： 3,000个具有相同产品但不同定价的经销商<br>
**解决方案**：一个目录，其中包含经销商特定的目录视图和价格手册

### 多位置retailer

**挑战**：每个位置的定价和库存不同<br>
**解决方案**：基于位置的目录视图以及特定于区域的策略

>[!NOTE]
>
>有关目录数据摄取和投放的详细信息，请参阅[开发人员文档](https://developer.adobe.com/commerce/services/optimizer/)。
