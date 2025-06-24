---
title: 用户管理
description: 了解如何管理 [!DNL Adobe Commerce Optimizer]中的用户。
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目(Adobe管理的SaaS基础架构)。"
source-git-commit: 02758aa5cc14af6d46bfc4bb7865fa37a787d4cb
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---

# 用户管理

要启用对[!DNL Adobe Commerce Optimizer]的访问权限，请从[Adobe Admin Console](https://adminconsole.adobe.com){target="_blank"}添加用户，并确保他们有权访问Commerce产品。

您可以将用户分配到以下任意角色：

- **用户** — 用户有权访问[!DNL Adobe Commerce Optimizer] UI以查看和管理目录视图和促销规则，以及跟踪绩效指标。

- [**开发人员**](https://helpx.adobe.com/enterprise/using/manage-developers.html#Adddevelopers){target="_blank"} — 开发人员具有用户权限和访问Adobe Developer Console的权限。 这意味着他们可以创建项目并配置凭据以使用[!DNL Adobe Commerce Optimizer] API和SDK等开发人员工具以及App Builder和API Mesh等Adobe可扩展性工具。

- **管理员** — 有三种不同类型的管理员角色：
   - [系统管理员](https://helpx.adobe.com/enterprise/using/admin-roles.html){target="_blank"} — 系统管理员可以通过Adobe Admin Console访问组织中的所有产品和产品配置文件。
   - [产品管理员](#add-a-product-admin) — 产品管理员可以在[!DNL Adobe Admin Console]中[管理产品](#add-users-and-admins)的用户、角色和权限。
   - [产品配置文件管理员](#add-users-developers-and-product-profile-admins) — 产品配置文件管理员可以在[!DNL Adobe Admin Console]中管理产品的用户。

## 添加产品管理员

1. 导航到[Admin Console](https://adminconsole.adobe.com)，然后使用您的Adobe ID登录。

1. 选择您的组织。

1. 在&#x200B;[!UICONTROL **产品**]&#x200B;选项卡的&#x200B;[!UICONTROL **产品和服务**]&#x200B;下，选择&#x200B;[!UICONTROL **Adobe Commerce as a Cloud Service — 后端**]&#x200B;产品。

   ![选择产品](../cloud-service/assets/backend.png){width="600" zoomable="yes"}

1. 选择&#x200B;[!UICONTROL **管理员**]&#x200B;选项卡。

1. 单击&#x200B;[!UICONTROL **添加管理员**]。

1. 输入要添加为管理员的用户名或电子邮件地址，然后单击&#x200B;[!UICONTROL **保存**]。

## 添加用户、开发人员和产品配置文件管理员

>[!BEGINSHADEBOX “先决条件”]
>
用户管理需要以下设置：

- 为[!DNL Adobe Commerce Optimizer]设置的IMS组织
- 具有系统或产品管理员角色的同一IMS组织中的Adobe Experience Cloud帐户

>[!ENDSHADEBOX]

使用以下说明将用户和开发人员添加到[!DNL Commerce Cloud Manager]，您可以在其中管理Commerce实例。

1. 导航到[Adobe Admin Console](https://adminconsole.adobe.com)并使用您的Adobe ID登录。

1. 选择您的组织。

1. 在&#x200B;[!UICONTROL **产品**]&#x200B;选项卡的&#x200B;[!UICONTROL **产品和服务**]&#x200B;下，选择&#x200B;[!UICONTROL **Adobe Commerce as a Cloud Service — 后端**]&#x200B;产品。

   ![选择产品](../cloud-service/assets/backend.png){width="600" zoomable="yes"}

1. 单击&#x200B;[!UICONTROL **默认 — Cloud Manager**]&#x200B;产品配置文件。

1. 选择&#x200B;[!UICONTROL **用户**]、[!UICONTROL **开发人员**]&#x200B;或&#x200B;[!UICONTROL **管理员**]&#x200B;选项卡，然后单击&#x200B;[!UICONTROL **添加用户**]、[!UICONTROL **添加开发人员**]&#x200B;或&#x200B;[!UICONTROL **添加管理员**]。

   从此屏幕添加的管理员已分配给[产品配置文件管理员](#understanding-roles)组。

   ![选项卡选择](../cloud-service/assets/tab-select.png){width=600 zoomable="yes"}

1. 输入要添加为管理员的用户名或电子邮件地址，然后单击&#x200B;[!UICONTROL **保存**]。

## 批量用户管理

您可以使用以下方法之一更高效地添加多个用户：

- 使用Adobe Admin Console中的&#x200B;**通过CSV添加用户**&#x200B;功能执行[批量CSV上传](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html){target="_blank"}。
- 通过创建[用户组](https://helpx.adobe.com/enterprise/using/user-groups.html){target="_blank"}将多个用户添加到角色。 然后，将&#x200B;[!UICONTROL **Adobe Commerce as a Cloud Service — 后端**]&#x200B;产品添加到用户组。

