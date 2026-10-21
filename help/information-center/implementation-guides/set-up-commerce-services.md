---
title: 设置Commerce服务
description: 了解如何使用Adobe Commerce Services Connector将Commerce连接到促销服务，以及将Magento Open Source连接到支付服务。
role: Admin, Developer
feature: Integration, Configuration
recommendations: noCatalog
autotag-review: '2026-10-20T11:14:04.410Z'
TQID: 'https://experienceleague.adobe.com/yyUDw1y5CYHxdLlC3bNo0DKK0byamPAKUjK-wwxVEX4'
product_v2:
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
subfeature_v2:
  - id: a1d22079-48b9-5e69-9ee6-eb236068ef34
    internal-label: Search
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%
---

# 设置Commerce服务

云基础架构上的Adobe Commerce和内部部署项目通过Commerce Services Connector连接到诸如[!DNL Catalog Service]、[!DNL Live Search]、[!DNL Product Recommendations]和[!DNL Payment Services]之类的服务。 在[!DNL Adobe Commerce as a Cloud Service]上，此连接被自动配置。

Magento Open Source使用[!DNL Payment Services]的Commerce Services Connector。 [!DNL Catalog Service]、[!DNL Live Search]和[!DNL Product Recommendations]需要Adobe Commerce并且不适用于Magento Open Source。

>[!NOTE]
>
>Adobe Commerce Optimizer以本机方式提供目录和促销功能，而不使用单独的[!DNL Live Search]、[!DNL Catalog Service]和[!DNL Product Recommendations]服务。 其目录同步不需要Commerce服务连接器。 Commerce后端上的其他集成（如[!DNL Payment Services]和[!DNL Data Connection]）仍需要连接器。 请参阅[为优化程序设置启用Adobe Commerce Optimizer](enable-aco.md)。


## 快速入门

1. 查看[Commerce Services Connector](/help/landing/saas.md)文档以获取和配置您的API密钥。

1. 有关通过连接器提供的各项服务，请参阅[Adobe Commerce Services Guides](/help/landing/home.md)。

## 相关指导

- [配置付款](configure-payments.md)
- [连接AEM Assets](connect-aem-assets.md)
- [与Adobe Experience Platform集成](integrate-aep.md)
