---
title: 批量数据迁移工具
description: 了解如何使用批量数据迁移工具将数据从云实例上的现有Adobe Commerce迁移到 [!DNL Adobe Commerce as a Cloud Service]。
feature: Cloud
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目（Adobe管理的SaaS基础架构）。"
role: Developer
level: Intermediate
exl-id: 81522de9-df54-4651-b8ed-58956376af86
autotag-review: '2026-07-22T19:18:39.433Z'
TQID: 'https://experienceleague.adobe.com/tkCFabZpBKu-W34wsufHlVIWzCUE8FKm4kK7qZahxBU'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
subfeature_v2:
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 4c0eca0039bab7d015144dd9ac3885a0b2be0563
workflow-type: tm+mt
source-wordcount: 924
ht-degree: 0%

---

# 批量数据迁移工具

>[!IMPORTANT]
>
>批量数据迁移工具当前处于早期访问状态。 只能通过Commerce部署工程(CDE)参与流程提供访问。

批量数据迁移工具使系统集成商能够将第一方核心商务数据从[!DNL Adobe Commerce on Cloud]或内部部署安装迁移到[!DNL Adobe Commerce as a Cloud Service]。

批量数据迁移工具是一个基于Docker的CLI，系统集成商可在他们自己的迁移计算机上运行。 它连接到源实例，提取第一方核心商务数据，将其上传到Adobe的迁移服务（Commerce数据迁移服务），并监视到完成的进度。

所有命令都在本地运行，因此您可以控制何时开始迁移、何时应用维护模式以及何时运行每个阶段。

## 迁移工作流

该工具端到端地管理以下阶段：

- **数据提取** — 从源实例（[!DNL Adobe Commerce on Cloud]或本地）提取第一方核心商务数据。
- **数据加载** — 将提取的数据加载到目标[!DNL Adobe Commerce as a Cloud Service]实例中。
- **数据完整性验证** — 执行自动化的迁移后检查，包括REST和GraphQL API比较以及记录计数验证。

>[!NOTE]
>
>目前，批量数据迁移工具仅支持迁移第一方核心商务数据。 当前不支持自定义数据迁移。 配置设置（存储设置、系统配置）不会自动迁移，必须在迁移之前在目标实例上单独进行设置。

## 架构

批量数据迁移工具遵循分布式架构，可实现安全高效的数据迁移。 此工具可帮助系统集成商将数据从现有[!DNL Adobe Commerce on Cloud or on-premises instance]迁移到[!DNL Adobe Commerce as a Cloud Service]。 有关迁移过程的详细信息，请参阅[迁移概述](../overview.md)。

下图详细介绍了使用批量数据迁移工具的架构和端到端数据流。

![显示PaaS到SaaS数据流的批量数据迁移工具体系结构图](../../assets/bulk-data-diagram.png){zoomable="yes"}

### 组件

| 组件 | 角色 |
| --------- | ---- |
| **批量数据迁移工具** | 系统集成商在迁移计算机上运行的基于Docker的CLI，它通过从源中读取架构和数据，将提取的数据上传到Adobe的迁移服务并驱动状态转换来协调整个管道。 |
| **Source实例（云端或内部部署的Commerce）** | 迁移源。 该工具通过REST和GraphQL API进行连接，并通过SSH通道([!DNL Adobe Commerce on Cloud])进行连接，或通过直接数据库连接（本地）进行连接，以进行数据提取。 |
| **Commerce数据迁移服务(CDMS) API** | Adobe管理的REST API可注册迁移、协调状态转换并为上传提取的数据提供安全端点。 迁移工具使用`.env`配置中的CDMS端点URL和IMS凭据连接到此API。 |
| **Commerce数据迁移服务(CDMS)工作程序** | Adobe管理的后台服务，它将提取的数据加载到Target实例中并运行加载后完整性验证。 |
| **[!DNL Adobe Commerce as a Cloud Service]** | 基于SaaS的Adobe Commerce版本和您的迁移目标。 接收加载的数据并公开在完整性验证期间使用的目录、实时搜索和定价规则服务。 |

### 数据流

数据按以下顺序在组件中移动：

1. 批量数据迁移工具通过[!DNL Adobe Commerce on Cloud]的SSH通道或本地的直接数据库连接，从源实例读取数据库架构和数据。
1. 该工具会注册迁移，并通过CDMS API上传提取的数据。
1. CDMS工作进程将数据加载到目标[!DNL Adobe Commerce as a Cloud Service]租户。
1. [!DNL Adobe Commerce as a Cloud Service]摄取加载的目录数据并生成目录索引。
1. Commerce数据迁移服务(CDMS)工作进程通过数据库校验和比较、REST和GraphQL跨以下服务验证加载的数据：

   - **目录** (GraphQL) — 产品和类别数据。
   - **实时搜索** (REST) — 搜索索引正确。
   - **定价规则** (REST) — 价格和规则数据。

1. 该工具在整个过程中轮询迁移状态，并在完成时检索最终迁移报告。


## 参与生命周期

批量数据迁移工具的访问完全通过Commerce部署工程(CDE)项目提供。 该工具不可公开访问。

典型的项目生命周期是：

1. **CDE发现** — 完成初始范围设定调用，评估数据足迹和复杂性，并完成范围设定调查表。
1. **交易签名** — 已签订商业协议并已确认迁移范围。 在此阶段，您有权访问迁移工具。
1. **CDE联合创新与支持** — 与Adobe合作，在您的环境中安装该工具并执行测试迁移。
1. **上线** — 运行生产直接转换迁移并完成数据完整性验证。

## 工具分发

该工具作为CDE参与的一部分分发。 您的Adobe代表提供了工具包，其中包括：

- 基于Docker的CLI和构建配置
- `.example.env`配置模板，其中包含所有必需环境变量的文档
- 全面的技术文档，涵盖该工具的体系结构、配置参考、自定义转换和测试框架以及故障排除指南

有关详细的设置和操作说明，请参阅工具分发包中包含的文档。

## 迁移指南

以下页面演示了从准备到执行的整个迁移生命周期。 要全面了解迁移过程，请按照以下顺序查看它们：

1. [客户准备工作清单](readiness-checklist.md) — 在请求工具访问权限之前，请确认参与情况、迁移计算机、源和目标先决条件。
1. [验证迁移服务访问权限](cdms-access.md) — 获得对该工具的访问权限后，根据Commerce数据迁移服务(CDMS) API验证网络可达性、IMS身份验证和租户授权。
1. [运行批量数据迁移](migration-guide.md) — 配置该工具，准备网络和实例，然后开始迁移。

有关完整配置参考、自定义转换和测试框架以及故障排除指南，请参阅工具分发包中包含的文档。
