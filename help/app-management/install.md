---
title: 安装和访问 [!DNL App Management]
description: 使用Adobe Commerce [!DNL App Management]的先决条件和访问要求
feature: App Builder, Extensibility, Integration
source-git-commit: 86c0945bbb0a562de1b66d420dec2a05d4d81e5f
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# 安装和访问[!DNL App Management]

[!DNL App Management]在Commerce管理员中可用于符合条件的Commerce实例。 可用性取决于您的部署类型。

## 可用性

满足以下要求后，请在下面为您的部署类型选择对应的选项卡，以查看[!DNL App Management]是需要安装还是已在您的实例上可用。

## 先决条件

在关联应用程序之前，请确保您满足以下条件：

| 要求 | 描述 |
|-------------|-------------|
| **管理员访问权限** | 具有[!DNL App Management]权限的Commerce管理员 |
| **已部署应用程序** | App Builder应用程序已部署到您的组织并准备好连接 |
| **组织访问权限** | 访问部署应用程序的Adobe组织 |

>[!BEGINTABS]

>[!TAB Adobe Commerce as a Cloud Service]

[!DNL App Management]在[!DNL Adobe Commerce as a Cloud Service]上自动可用。 无需安装。 [在管理员中启用它](#access-app-management)，并开始关联应用。

>[!TAB 云端(PaaS)和内部部署上的Adobe Commerce]

* **Adobe Commerce 2.4.8及更高版本**—[!DNL App Management]会自动包含在内。 无需安装。

* **Adobe Commerce 2.4.5到2.4.7** — 使用编辑器安装[!DNL Admin UI SDK]（包括[!DNL App Management]）：

  ```bash
  composer require "magento/commerce-backend-sdk": ">=3.3"
  ```

  然后运行：

  ```bash
  composer update
  bin/magento setup:upgrade
  bin/magento indexer:reindex
  bin/magento cache:clean
  ```

有关详细信息，请参阅[安装或更新Adobe Commerce Admin UI SDK](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/installation/){target="_blank"}。

>[!ENDTABS]

## 访问[!DNL App Management]

1. 登录到Commerce管理员。

1. 导航到&#x200B;**[!UICONTROL Apps]** > **[!UICONTROL App Management]**。

将显示[!DNL App Management]视图。 在这里，您可以关联、配置和管理App Builder应用程序。

## 安装App Builder应用程序

如果您需要从Adobe Exchange安装App Builder应用程序（例如，预建的集成或市场应用程序），请参阅[从Adobe Exchange安装App Builder应用程序](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/install-app-builder-app){target="_blank"}以了解分步说明。

安装并部署应用程序后，使用[!DNL App Management]将其与您的Commerce实例[关联并配置其设置。](manage-app.md#associate-an-app)

## Commerce webhook和应用程序

某些App Builder应用程序使用[Adobe Commerce webhook](https://developer.adobe.com/commerce/extensibility/webhooks/)，以便当某些事件发生时（例如，在保存产品后），Commerce可以通过HTTP调用您的应用程序。 Webhook端点和订阅逻辑由&#x200B;**应用程序开发人员**&#x200B;在生成和部署应用程序时定义；商店管理员不会在应用程序管理中单独配置Webhook。

在您[将应用程序](https://experienceleague.adobe.com/en/docs/commerce/app-management/manage-app/manage-app)与您的Commerce实例关联并完成应用程序的任何设置指令后，webhook行为将遵循应用程序的实施。

如果[!DNL App Management]无法触发应用程序的验证终结点（例如，无法访问URL或响应不符合要求），则您可能会在[!DNL App Management]仪表板中看到类似以下内容的错误：

![Webhook验证错误](assets/webhook-validation-error.png){width="600" zoomable="yes"}

请与&#x200B;**应用程序开发人员**&#x200B;合作更正webhook配置或部署，以便成功验证。

**应用程序开发人员**。 要实施来自App Builder的webhook订阅和处理程序响应，请参阅Commerce可扩展性开发人员文档中的[Webhooks](https://developer.adobe.com/commerce/extensibility/app-management/installation/webhooks/)和GitHub上的[`@adobe/aio-commerce-lib-webhooks`](https://github.com/adobe/aio-commerce-sdk/tree/main/packages/aio-commerce-lib-webhooks)包。
