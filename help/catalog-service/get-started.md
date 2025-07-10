---
title: 开始使用 [!DNL Catalog Service]
description: 了解如何访问 [!DNL Catalog Service] 并与前端应用程序和第三方服务集成。
role: Admin, Developer
source-git-commit: 3a6a81fa03f13c24ac08041c39452c553aa54f55
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---


# 开始使用[!DNL Catalog Service]

启用[!DNL Catalog Service]后，您可以访问该服务，并使用它从Adobe Commerce实例中检索目录数据，如产品和类别信息。 该服务作为GraphQL API提供，您可以从Commerce管理员或从支持GraphQL查询的任何前端应用程序访问该服务。

## 访问服务

[!DNL Catalog Service]可用作GraphQL API，您可以从Commerce管理员或任何支持GraphQL查询的前端应用程序访问它。 该服务在SaaS和PaaS环境中均可用。


仅[!BADGE PaaS]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于云项目(Adobe管理的PaaS基础架构)和内部部署项目上的Adobe Commerce 。"}

| 环境 | 端点 |
|------------ | ----------: |
| **正在测试** | `https://catalog-service-sandbox.adobe.io/graphql` |
| **生产** | `https://catalog-service.adobe.io/graphql` |

仅[!BADGE SaaS]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目(Adobe管理的SaaS基础架构)。"}

| 环境 | 端点 |
| ------------ | --------:|
| 测试 | `https://na1-sandbox.api.commerce.adobe.com/{{tenant-id}}/graphql` |
| 生产（尚不可用） | `https://na1.api.commerce.adobe.com/{{tenant-id}}/graphql` |

SaaS端点的&#x200B;**URL结构**

```text
https://<region>-<environment>.api.commerce.adobe.com/<tenantId>/graphql
```

- `<region>`是部署实例的云区域。
- `<environment>`是环境类型，如`sandbox`。 如果环境是生产环境，则忽略此值。
- `<tenantId>`是Adobe Experience Cloud中您组织的特定实例的唯一标识符。

有关使用目录服务GraphQL API的详细信息，请参阅[Adobe Commerce开发人员](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)文档中的&#x200B;*Adobe Commerce目录服务指南*。


## 与Headless店面或第三方服务集成

要与Headless店面集成，您必须更新店面配置以启用店面和[!DNL Catalog Service]之间的通信以检索产品和类别数据。

如果您在Edge Delivery Services上使用Adobe Commerce店面，请将目录服务端点添加到店面配置。 有关详细信息，请参阅[Edge Delivery Services文档](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/#storefront-configuration)。

有关其他集成，请参阅项目设置文档，了解有关如何配置服务和后端数据源之间的集成的详细信息。


### 防火墙配置

要允许[!DNL Catalog Service]通过防火墙，请将`commerce.adobe.io`添加到允许列表。

## 目录服务和API网格

适用于Adobe Developer App Builder[的](https://developer.adobe.com/graphql-mesh-gateway/gateway/overview/)API Mesh使开发人员能够使用Adobe IO将专用或第三方API以及其他接口与Adobe产品集成。

有关安装和配置详细信息，请参阅[[!DNL Catalog Service] 和API Mesh](mesh.md)主题。

## 使用数据管理功能板

使用[数据管理功能板](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard)监视[!DNL Catalog Service]与Adobe Commerce实例之间的数据同步。 功能板提供了有关数据传输流程的洞察，包括数据导出的状态和同步产品的列表。
