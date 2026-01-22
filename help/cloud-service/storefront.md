---
title: 设置您的店面
description: 了解如何运行基架工具来设置 [!DNL Adobe Commerce as a Cloud Service] 店面。
feature: Storefront
role: Developer
level: Beginner
exl-id: 02928dc4-1777-483e-b0ee-b04fc813864d
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目(Adobe管理的SaaS基础架构)。"
source-git-commit: 0cd9749574460374a8fe875f1eff54f2a4a8d614
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# 设置您的店面

要为[!DNL Adobe Commerce Storefront] (SaaS)设置由[!DNL Edge Delivery Services]提供支持的[!DNL Adobe Commerce as a Cloud Service]，请完成以下步骤。

有关更可自定义的详细演练，请参阅[店面文档](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/)。

1. 打开[站点创建者工具](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator)。

1. 选择&#x200B;**[!UICONTROL Create New Site (Code & Content)]**。

1. 输入要创建店面代码存储库的&#x200B;**[!UICONTROL Github Organization/Username]**。

1. 输入&#x200B;**[!UICONTROL Site Name]**。

1. 在&#x200B;**[!UICONTROL Commerce GraphQL Endpoint (optional)]**&#x200B;字段中，输入您的[!DNL Adobe Commerce as a Cloud Service] (SaaS) GraphQL端点，在[创建实例](./getting-started.md#create-an-instance)后，您可以在Commerce Cloud Manager中访问该端点。

   或者，如果您使用的是[[!DNL API Mesh]](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic)，请在[!DNL API Mesh]字段中输入您的&#x200B;**[!UICONTROL Commerce GraphQL Endpoint (optional)]** GraphQL端点。 有关详细信息，请参阅[创建网格](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic/create-mesh)。

1. 单击&#x200B;**[!UICONTROL Create Site]**。 按照屏幕上的说明授权访问GitHub存储库。

该过程完成后，您可以使用以下方法自定义您的店面：

* 自定义您的代码： `https://github.com/<username or org>/<repo name>`
* 编辑您的内容： `https://da.live/#/<username or org>/<repo name>`
* 管理您的配置： `https://da.live/sheet#/<username or org>/<repo name>/configs-stage`
* 预览店面： `https://main--<repo name>--<username or org>.aem.page/`

## 后续步骤

有关更多信息，请参阅以下文章：

* [更新店面内容](./use-cases.md#update-storefront-content) — 管理和显示店面上的内容和数据。
* [情境实验](./use-cases.md#contextual-experimentation) — 在店面中创建和管理实验。
* [生成变体](./use-cases.md#generate-variations) — 使用创作AI自动生成高质量的内容。
* [Adobe Commerce Storefront文档](https://experienceleague.adobe.com/developer/commerce/storefront/) — 获取有关更新网站内容以及与Commerce前端组件和后端数据集成的详细信息。
* [配置服务](https://www.aem.live/docs/config-service-setup) — 了解如何从`config.json`迁移店面配置以使用配置服务，该服务支持高级用例，如重写配置和覆盖。
