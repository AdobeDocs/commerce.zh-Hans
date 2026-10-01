---
title: B2B共享目录投影
description: 了解B2B连接器如何将Adobe Commerce B2B共享目录项目到受保护的Commerce Optimizer目录视图中，以及店面如何解析和授权买方访问。
feature: Integration, Configuration
role: Admin, Developer
level: Intermediate
TQID: 'https://experienceleague.adobe.com/b37PBjcVQXRSLrB6c7nEf3A3U5cuLs1lQzwPUbp9fdA'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
feature_v2:
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
    internal-label: Security
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
subfeature_v2:
  - id: 3c398179-d35a-51ba-b317-6c5b95feef5e
    internal-label: Logs
  - id: a1d22079-48b9-5e69-9ee6-eb236068ef34
    internal-label: Search
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
source-git-commit: a3ade1a31d3c2905b601f71bda118de89c43cf59
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%
---
# B2B共享目录投影

[!DNL Adobe Commerce Optimizer Connector for B2B]项目[!DNL Adobe Commerce]将共享目录和公司分配共享到受保护的[!DNL Adobe Commerce Optimizer]目录视图中。

## 基本同步和B2B投影

基础[!DNL Adobe Commerce Optimizer Connector]同步目录和定价信息源，将商店视图映射到目录源，将网站映射到价格手册，将客户组映射到价格手册。

[!DNL Adobe Commerce Optimizer Connector for B2B]将每个自定义共享目录的分类和价格投影到受保护的视图中。 Adobe Commerce使用买方的公司分配选择视图。 受限访问密钥验证已签名的请求，但不确定目录访问。 Adobe Commerce是连接器管理的目录、定价和B2B投影数据的记录系统。 在[!DNL Adobe Commerce Optimizer]配置中管理产品发现和推荐。

## 数据映射

B2B投影将同步的目录内容和定价与共享目录分类和公司分配上下文相结合。

![关系图将[!DNL Adobe Commerce]存储视图、定价、共享目录和公司分配映射到[!DNL Adobe Commerce Optimizer]](./assets/b2b-catalog-projection-mapping.svg){width="800"}中计划的专用目录视图

| [!DNL Adobe Commerce]数据 | [!DNL Adobe Commerce Optimizer]个结果 | 用途 |
| --- | --- | --- |
| 已启用商店视图和产品数据 | 目录源 | 提供本地化的产品内容。 |
| 网站和客户组定价 | 价格手册 | 提供适用的价格，但不授权访问 |
| 自定义共享目录分类 | 策略 | 将目录视图过滤到共享目录分类。 |
| 自定义共享目录和启用的商店视图 | 专用目录视图 | 为每个组合创建一个受保护的视图，以及适用的目录来源、策略和价格手册。 |
| 公司分配给共享目录 | 已解决的采购员上下文 | 允许经过身份验证的后端解析与买方公司关联的目录视图。 |
| 分配给受保护视图的受限制访问密钥 | 目录保护 | 授权请求访问受保护的目录视图，但不选择定价。 |

每个专用目录视图只能引用一个价格手册。 使用不同本地化的目录源时，具有相同网站和客户组定价上下文的商店视图可以共享价格手册。 连接器不会为每个共享目录创建价格手册。

默认共享目录不会投影为B2B专用目录视图。

## 运行时授权

采购员登录后，Commerce后端会验证会话，并使用采购员的公司分配和商店视图解析相应的目录视图和价格手册。

店面会随每个促销API请求发送目录视图ID、价格手册ID和签名令牌。 [!DNL Adobe Commerce Optimizer]根据分配给目录视图的受限制访问密钥验证JWT的RS256签名。 仅当令牌和密钥有效且未过期时，才会返回目录数据。

从购物者通过店面和Commerce后端到[!DNL Adobe Commerce Optimizer]](./assets/b2b-catalog-runtime-authorization.svg){width="700"}的B2B目录请求的运行时授权流![

对于私有目录请求，发送以下标头：

| 页眉 | 用途 |
| --- | --- |
| `AC-View-ID` | 标识目录视图。 |
| `AC-Price-Book-ID` | 标识要使用的价格手册。 |
| `AC-Catalog-View-Access-Token` | 携带已签名的JWT，该JWT授权对受保护目录视图的访问。 |

有关完整请求和令牌要求，请参阅[促销API身份验证](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api#authentication)和[验证对私有目录视图的访问权限](/help/optimizer/setup/private-catalog-view.md#verify-access-is-enforced)。

## 保护边界

目录保护仅涵盖目录和搜索请求。 它不能保护购物车、结账或订单操作。 在Adobe Commerce或关联交易系统中强制实施购买资格。

## 投影设置和监测

B2B连接器可以从[!DNL Adobe Commerce]中项目专用目录视图、策略、价格手册引用和受限访问密钥配置。 您无需手动创建这些连接器管理的投影对象。 有关设置说明，请参阅[开始使用B2B连接器](get-started-b2b-shared-catalogs.md)。

要监视预计的目录视图并协调配置偏移，请参阅[监视目录视图同步](catalog-view-sync-status.md)。 要管理分配的密钥，请参阅[管理B2B共享目录的受限访问密钥](restricted-access-keys.md)。
