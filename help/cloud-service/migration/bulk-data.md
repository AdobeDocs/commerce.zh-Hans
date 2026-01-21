---
title: 批量数据迁移工具
description: 学习如何使用批量数据迁移工具将现有的Adobe Commerce on Cloud实例中的数据迁移到 [!DNL Adobe Commerce as a Cloud Service]其他平台。
feature: Cloud
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe商务云服务和Adobe Commerce优化器项目（Adobe管理的SaaS基础设施）。"
role: Developer
level: Intermediate
exl-id: 81522de9-df54-4651-b8ed-58956376af86
source-git-commit: e582ce85b58b57922a8cdd63dbe32bd0f08c64f9
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 0%

---

# 批量数据迁移工具

批量数据迁移工具采用分布式架构，实现从PaaS环境到SaaS环境的安全高效数据迁移。 该工具帮助解决方案实施者将数据从现有的Adobe云端Commerce 实例（PaaS）迁移到 [!DNL Adobe Commerce as a Cloud Service] （SaaS）。 有关迁移流程的更多信息，请参见 [迁移概览](./overview.md)。

>[!NOTE]
>
>批量数据迁移工具仅支持迁移第一方核心商务数据。 目前不支持自定义数据迁移。

以下图像详细介绍了使用批量数据迁移工具的体系结构和关键组件。

![显示Paa到SaaS数据流的批量数据迁移工具体系结构图](../assets/bulk-data-diagram.png){zoomable="yes"}

## 迁移工作流程

批量数据迁移工作流程包含以下步骤：

1. 为迁移设置新环境。
1. 从旧系统复制你的数据。
1. 把你的数据迁移到新系统。
1. 将您的产品目录提供在新系统中。
1. 确认你的数据是否正确迁移。

以下各节详细描述了这些步骤。

## 访问批量数据迁移工具

批量数据迁移工具的可用性如下：

- **2026** 年第一季度（尚未提供）——批量数据迁移工具首次发布后，您可以通过提交支持工单访问该工具。
- **2026** 年第一季度（尚未开放）——批量数据迁移工具公开发布后，将可从本页面访问。

## 创建目标环境

解决方案实现者（SI）为迁移创建目标环境。 该环境存储从源实例迁移的数据。

首先，创建一个 [新的 [!DNL Adobe Commerce as a Cloud Service] （SaaS）实例](../getting-started.md#create-an-instance)。

### 配置提取工具

使用提取工具从源实例中提取数据。

1. 从Adobe提供的链接下载提取工具。
1. 在提取工具中设置以下环境变量：
   - 与现有MySQL数据库的连接详细信息
   - [!DNL Adobe Commerce as a Cloud Service]实例的目标租户ID
   - 您的IMS凭据，包括：
      - 客户端ID
      - 客户端密码
      - IMS范围
      - IMS URL - 基础 URL。 例如， `https://ims-na1.adobelogin.com/`。
      - IMS组织ID

   对于IMS范围和其他值，请在&#x200B;**Adobe Developer Console**&#x200B;的项目内的[凭据](https://developer.adobe.com/console/)部分中选择您的OAuth类型。 提取工具附带的`.example.env`文件中提供了详细信息。

### 提取数据

在运行提取工具之前，解决方案实施者必须通过以下方式建立连接到PaaS数据库的SSH隧道：

```bash
magento-cloud tunnel:open
```

然后运行提取工具，它将：

1. 连接到PaaS数据库，分析其模式，并与SaaS租户模式细节进行比较。
1. 基于PaaS和SaaS之间的通用模式元素生成提取和转换计划。
1. 使用目录数据管理服务（CDMS）提取数据。

### 装载数据

运行Adobe提供的加载数据工具。 此工具将：

1. 使用迁移帐户连接到SaaS租户数据库。
1. 生成加载计划。
1. 执行计划，将数据批量移动到SaaS租户数据库。
1. 处理目录介质并将其传输到目标环境。
1. 清除SaaS Redis缓存，并使租户的数据库索引失效。

### 目录数据摄取

数据加载完成后，目录数据会自动从SaaS租户数据库流向目录服务。

目录服务与实时搜索和产品推荐共享这些数据。 此过程不需要手动干预。 数据一旦导入完成，所有服务中都可以使用。

### 数据完整性验证

迁移后，CDMS 执行以下自动数据完整性检查，以确保迁移数据的准确性和完整性：

**基于API的验证**

在验证过程中，CDMS 将之前运行查询的 REST 和 GraphQL API 响应与目标实例的相应记录进行比较。 任何差异都会在迁移状态中显示。

**数据库级验证**

在验证过程中，CDMS 统计提取记录的数量，并将其与加载的记录数量进行比较。

**按需验证（可选）**

您也可以手动触发对所有系统记录的全面验证：

>[!NOTE]
>
>该过程资源密集，应仅在沙盒环境中使用。

完整的核查包括：

- 基于API的完整验证，使用所有预提取的REST和GraphQL API响应
- 发现的任何不一致的详细报告
