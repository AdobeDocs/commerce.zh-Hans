---
title: 安全架构和数据流
description: 了解Adobe Commerce as a Cloud Service的安全架构和数据流。
role: Admin, Developer, Leader
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目（Adobe管理的SaaS基础架构）。"
autotag-review: '2026-06-18T16:16:18.600Z'
TQID: 'https://experienceleague.adobe.com/2yK-VVec98nFH9LPpfSe4kQ2YvQr2yy3G0Rym5-HCbI'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2: id: ba9e5be9-7de1-4f71-a5d2-baead0e425eeid: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
subfeature_v2: id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8id: f8a45b24-4be7-4f1b-909b-60d06b483a20
level_v2: id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: 15a99ce130efaf3a35968cfc01747fe1b6ab93c9
workflow-type: tm+mt
source-wordcount: 387
ht-degree: 0%

---


# 安全架构和数据流

以下示例说明数据通常如何在[!DNL Adobe Commerce as a Cloud Service]中流动：

![Adobe Commerce as a Cloud Service数据流程图](../assets/data-flow-1.png)

## 数据流描述

**步骤1**：购物者在其浏览器中键入商户店面的URL，该URL将发送到Commerce店面的内容交付网络（外部CDN）。

**步骤2**：如果已缓存网站URL，则Storefront CDN会将其返回给购物者。 如果尚未缓存（如果这是第一个资源请求，则可能会发生这种情况），则外部CDN会将购物者的请求转发到内部CDN，并缓存后续请求的响应。

**步骤2a**：如果请求是针对图像或视频的，则它会发送到[!DNL Product Visuals]以进行履行并返回店面。

**步骤3**：如果站点URL缓存在内部CDN上，则会从该缓存返回。 如果不存在，则将其发送到[!DNL API Mesh]，并为后续请求缓存响应。

**步骤4**： [!DNL API Mesh]充当业务流程层，并决定是向[!DNL Adobe Commerce as a Cloud Service]还是向第三方系统发送请求以完成该请求。

>[!NOTE]
>
>只有在自定义了网格配置的情况下，[!DNL API Mesh]才会向第三方系统发送请求。

**步骤5**：发送给[!DNL Adobe Commerce as a Cloud Service]的请求将通过Web应用程序防火墙(WAF)阻止可疑或恶意请求。 如果所请求的URL缓存在[!DNL Commerce] CDN中，则会从该缓存中传送该URL。 如果未缓存，则从一项或多项[!DNL Adobe Commerce as a Cloud Service]微服务（例如foundation、search和recommendations）返回它，然后缓存以供将来请求使用。

**步骤5a**：如果将请求发送到第三方系统，则将返回响应[!DNL API Mesh]。

**步骤5b**：如果请求用于付款处理，则付款提供商会在店面中呈现iframe，以便购物者安全地输入信用卡信息并完成付款交易。

**步骤6**：[!DNL API Mesh]收到来自[!DNL Adobe Commerce as a Cloud Service]或第三方服务的响应后，这些响应将拼合到一个统一的图形中，并返回到[!DNL Commerce Storefront]以服务购物者的请求。
