---
title: 目录源
description: 了解什么是目录源，以及它们如何定义产品、属性和类别的权威范围，以便进行搜索、过滤和排序行为。
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和 [!DNL Adobe Commerce Optimizer] 项目（Adobe管理的SaaS基础架构）。"
autotag-review: '2026-06-09T19:36:23.516Z'
TQID: 'https://experienceleague.adobe.com/MiLbuYx6Pf95n3jvrgvou05Ery9XHXskx8p6KrN6CYg'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b23e006f-0a29-4f1d-8fd0-77aa56f3d12b
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 94ba07437d532d0d101c166f58114c2aa0bd4be4
workflow-type: tm+mt
source-wordcount: 446
ht-degree: 0%

---

# 目录源

目录源代表产品、属性和类别的权威范围。 它们通常映射到语言、受众或原始系统边界，并决定搜索、过滤和排序行为。

## 目录源与相关概念

了解目录源如何与其他[!DNL Adobe Commerce Optimizer]概念相关联，有助于您正确建模数据：

* **目录源** — 提供产品信息的基础数据上下文。 目录源通常是区域设置（例如，`en-US`、`fr-CA`）或外部系统，如PIM或ERP。 产品、属性元数据和类别均按目录源规定作用域。 将目录源视为&#x200B;*其中*&#x200B;原始目录数据来自，以及&#x200B;*它对产品发现（搜索结果、筛选和排序行为）有何影响*。

* **[目录视图](catalog-view.md)** — 针对特定业务需求配置的目录视图。 创建目录视图时，选择要使用的目录源（或区域设置），然后添加[策略](policies.md)以筛选可见的产品，并链接[价格手册](pricebooks.md)以控制定价。 单个目录源可以为多个目录视图提供支持（例如，一个`en-US`源具有不同的品牌或区域的单独目录视图）。 将目录视图视为&#x200B;*如何*&#x200B;向店面、渠道或受众公开该数据。

* **[目录层](catalog-layer.md)** — 在基本目录数据上应用的层，用于修改产品属性（名称、描述、图像、元数据）而不更改源数据。 当差异必须仅影响店面显示时，请使用目录层，而不影响产品发现。

## 规则和限制

* 每个目录源都是通过数据摄取API摄取产品创建的。 有关详细信息，请参阅[开发人员文档 — 数据摄取](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/)。
* 产品唯一性由SKU +目录源决定。
* 购物者不能直接访问目录来源。 目录数据通过[目录视图](catalog-view.md)向店面公开。

## 建模导引

在决定如何构建目录源时，请遵循以下指南：

* 为每个目录语言创建单独的目录源。
* 当产品和属性的差异必须影响搜索、筛选或排序行为（例如，同一属性的不同可搜索性、可过滤性或Facet配置）时，请使用单独的目录源。
* 当产品和属性差异必须仅影响店面显示而非产品发现时，请使用[目录层](catalog-layer.md)。

>[!MORELIKETHIS]
>
> * [目录视图](catalog-view.md) — 在目录源之上配置筛选的定价视图
> * [目录层](catalog-layer.md) — 修改产品演示文稿，而不更改源数据
> * [策略](policies.md) — 为目录视图创建基于属性的筛选器
> * [价格手册](pricebooks.md) — 管理不同客户区段的定价结构

