---
title: Commerce信息中心管理
description: 了解Commerce信息中心的内部治理模型。 未发布到Experience League。
source-git-commit: a91925091da28cd0745923894a3faab0374f0a0c
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%
---

# Commerce信息中心治理

`TOC.md`中未列出该文档团队的内部引用，因此未将其发布到Adobe Experience League。

## 所有权

Adobe Commerce文档团队拥有信息中心。 它是在`Adobe-Enterprise-Docs/commerce.en`中创作的，存储库在`metadata.md`中列为`git-repo`。

没有哪个产品团队拥有它，因为它是跨产品的。 将特定于产品的更正上报给所属产品团队的文档联系人，而不是在此处进行修复。

## 信息中心的内容

| 属于此处 | 属于产品存储库 |
| --- | --- |
| 跨多个产品或服务的内容，如产品选择指南、跨产品实施历程、架构模式和白皮书 | 单个产品内容，如逐步配置、API/CLI/配置参考和故障排除 |
| 链接到权威产品文档的简短策划页面 | |

- 如果此处某个页面累积了单个产品的详细信息，请将其移至产品指南并链接到它。
- 信息中心不整合或迁移产品文档，也不记录各个产品功能。 在编写新内容之前，链接到现有的权威内容。

## 添加新内容

### 现有部分中的文章

1. 将文件添加到与部分匹配的文件夹中。
1. 在该部分下添加一个条目到`TOC.md`。

除正常的PR审查外，无需审批。

| 目录部分 | 文件夹 |
| --- | --- |
| 探索Commerce平台和服务 | `portfolio/`, `storefronts/`, `aem-assets/`, `apis/` |
| 角色入门 | `get-started/` |
| 见解和指导 | `guidance-and-insights/` |
| 架构 | `architecture-options/` |
| 迁移和采用 | `migration-adoption/` |
| 实施指南 | `implementation-guides/` |

### 见解和指导文章

1. 将`whitepaper-template.md`或`security-guidance-template.md`从`guidance-and-insights/templates/`复制到`guidance-and-insights/`。 未发布模板。 有关完整的创作过程，包括COMDOX摄取票证，请参阅[readme.md](guidance-and-insights/readme.md)。
1. 删除模板的占位符注释。
1. 当内容准备发布时，在分析和指导下添加`TOC.md`条目。

### 顶级部分

`TOC.md`中的新顶级组更改了指南的导航，因此需要IA审核。 联系Commerce IA审阅的所有者。 首先重用现有的部分，例如合作伙伴或支持内容的由角色开始使用。

### 已发布的URL

URL是从指南ID、`TOC.md`中的节ID（例如，`{#insights-and-guidance}`）和文件名生成的。 URL中未显示文件夹名称。 为每个部分指定一个唯一的ID，并确保没有两篇文章可解析为同一URL。

## 审核节奏

- **事件导向** — 在重命名、启动、弃用Commerce产品或其可用性更改时，查看“浏览Commerce平台和服务”、“按角色入门”、“架构”、“迁移和采用”以及“实施指南”部分。 例如，如果Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer获得集成，请查看它们。 这些页面首先会过时。
- **已计划** — 要捕获过时的术语、品牌或技术上的不准确之处，请每六个月运行一次自动内容审核和审查。

## 与帮助/登陆/的关系

`help/landing/` (“Adobe Commerce Services Guides”)是一个单独的指南，它不属于信息中心。 它主要关注Commerce服务，如目录服务、实时搜索、产品推荐和支付服务，以及指向它的信息中心链接，以了解详细信息。 重新处理或合并这两者是一个本指南未解决的后续决定。
