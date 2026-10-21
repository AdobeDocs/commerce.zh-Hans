---
title: 参考体系结构
description: 了解常用Adobe Commerce实施（如店面、服务和目录同步管道）的参考架构模式。
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T11:42:09.021Z'
TQID: 'https://experienceleague.adobe.com/GVbGyRZz8llMWcUykcXXZwWnTaAomHVCTcV3ft49IEc'
product_v2:
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
  - id: 8dc0e58b-adf0-51bb-8db5-bb36e3e656fb
    internal-label: Inventory
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
    internal-label: Commerce ecosystem
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%
---

# 参考体系结构

以下文档跨不同的部署模型和用例提供了Adobe Commerce平台和服务的参考架构模式。

- [Adobe Commerce as a Cloud Service架构](/help/cloud-service/overview.md#architecture)
- [Adobe Commerce企业参考架构](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/architecture/enterprise-blueprint){target="_blank"}
- [Adobe Commerce店面架构](https://experienceleague.adobe.com/en/tools/commerce-storefront/get-started/architecture/){target="_blank"}
- [云基础架构架构上的Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/architecture/cloud-architecture){target="_blank"}

## 由Edge Delivery Services提供支持的店面

在Adobe Commerce样板中构建的店面，使用插入组件和内容块，连接到Adobe Commerce或[!DNL Adobe Commerce Optimizer]作为后端。 查看[Adobe Commerce店面概述](https://experienceleague.adobe.com/en/tools/commerce-storefront/)。

- [Adobe Commerce店面架构](https://experienceleague.adobe.com/en/tools/commerce-storefront/get-started/architecture/)

## 目录同步管道

用于在Adobe Commerce和Adobe Commerce服务（Commerce Optimizer、实时搜索、目录服务、产品推荐和其他连接的[Commerce服务](../../landing/home.md)）之间保持目录、价格和库存数据同步的数据流。

- 对于Adobe Commerce as a Cloud Service、云基础架构或内部部署，请参阅[将数据与SaaS数据导出同步](/help/data-export/sync-overview.md)

- 对于云基础架构上的Adobe Commerce或使用Adobe Commerce Optimizer Connector配置的内部部署，请参阅[连接器同步管道](/help/aco-connector/connector-sync-pipeline.md)。


## 相关指导

- [实施体系结构](implementation-architectures.md)
