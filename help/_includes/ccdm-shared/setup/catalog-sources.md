---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%
---
目录源代表产品、属性和类别的权威范围。 它们通常映射到语言、受众或原始系统边界，并决定搜索、过滤和排序行为。

## 目录源与相关概念

了解目录源如何与其他Merchandising Services概念相关联，有助于您正确建模数据：

* **目录源** — 提供产品信息的基础数据上下文。 目录源通常表示区域设置（例如`en-US`、`fr-CA`）或由外部系统（如PIM或ERP）提供的数据上下文。 产品、属性元数据和类别都按目录源规定范围。 目录源定义原始目录数据的来源及其对产品发现（搜索结果、筛选和排序行为）的影响。

* **[目录视图](/help/optimizer/setup/catalog-view.md)** — 针对特定业务需求配置的目录视图。 目录视图选择目录源（或区域设置），应用[策略](/help/optimizer/setup/policies.md)以筛选产品可见性，并将[价格手册](/help/optimizer/setup/pricebooks.md)与视图关联。 单个目录源可以为多个目录视图提供支持（例如，一个`en-US`源具有不同的品牌或区域的单独目录视图）。 将目录视图视为&#x200B;*如何*&#x200B;向店面、渠道或受众公开该数据。

* **[目录层](catalog-layer.md)** — 在基本目录数据上应用的层，用于修改产品属性（名称、描述、图像、元数据）而不更改源数据。 当差异必须仅影响店面显示时，请使用目录层，而不影响产品发现。

## 如何填充目录源

目录源是通过目录数据摄取填充的。 如何提供这些数据取决于您的实施：

- **具有CCDM的Adobe Commerce as a Cloud Service** — 本机同步提供来自Commerce Foundation的目录数据。 在Commerce Foundation中管理基础产品和商店视图配置，并在[数据同步](data-sync.md)工作区中监视同步。 无需单独的数据摄取API集成。
- **具有第三方后端的Adobe Commerce Optimizer** — 您的集成通过[数据摄取API](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/)提供产品和目录源信息。


## 规则和限制

* 当Merchandising Services数据层首次接收新区域设置或源系统的目录数据时，将创建目录源。
* 产品唯一性由SKU +目录源决定。
* 购物者不能直接访问目录来源。 目录数据通过[目录视图](catalog-view.md)向店面公开。

## 建模导引

在规划目录结构时，请遵循以下指南。 对于带有CCDM的Adobe Commerce as a Cloud Service，请在Commerce Foundation中管理基础配置，而不是通过单独的摄取集成创建目录源。

* 为每个目录语言使用单独的目录源。
* 当产品和属性差异必须影响搜索、过滤或排序行为（如不同的可搜索性或可过滤性设置）时，请使用单独的目录源。
* 当产品和属性差异必须影响产品呈现方式而不更改搜索、筛选或排序行为时，请使用[目录层](catalog-layer.md)。

>[!MORELIKETHIS]
>
> * [目录视图](catalog-view.md) — 在目录源之上配置筛选的定价视图
> * [目录层](catalog-layer.md) — 修改产品演示文稿，而不更改源数据
> * [策略](policies.md) — 为目录视图创建基于属性的筛选器
> * [价格手册](/help/optimizer/setup/pricebooks.md) — 管理不同客户区段的定价结构
> * [受限访问密钥](restricted-access-keys.md) — 使用签名令牌身份验证保护目录视图
