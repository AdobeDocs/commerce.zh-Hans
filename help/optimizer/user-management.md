---
title: User和Identity Management
description: 了解如何创建和管理 [!DNL Adobe Commerce Optimizer]的用户以及分配用户角色。
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目(Adobe管理的SaaS基础架构)。"
exl-id: 9ab2118d-b7e3-4e2e-adac-8f3950fe1824
source-git-commit: b88406169191cb9d4f0d2b5ef113703f5afcd589
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 0%

---

# 用户管理

要启用对[!DNL Adobe Commerce Optimizer]的访问权限，请从[Adobe Admin Console](https://adminconsole.adobe.com){target="_blank"}添加用户，并确保他们有权访问Commerce产品。

您可以将用户分配到以下任意角色：

- **用户** — 用户有权访问[!DNL Adobe Commerce Optimizer] UI以查看和管理目录视图和促销规则，以及跟踪绩效指标。

- [**开发人员**](https://helpx.adobe.com/enterprise/using/manage-developers.html#Adddevelopers){target="_blank"} — 开发人员具有用户权限和访问Adobe Developer Console的权限。 这意味着他们可以创建项目并配置凭据以使用[!DNL Adobe Commerce Optimizer] API和SDK等开发人员工具以及App Builder和API Mesh等Adobe可扩展性工具。

- **管理员** — 有三种不同类型的管理员角色：
   - [系统管理员](https://helpx.adobe.com/enterprise/using/admin-roles.html){target="_blank"} — 系统管理员可以通过Adobe Admin Console访问组织中的所有产品和产品配置文件。
   - [产品管理员](#add-a-product-admin) — 产品管理员可以在[中](#add-users-and-admins)管理产品[!DNL Adobe Admin Console]的用户、角色和权限。
   - [产品配置文件管理员](#add-users-developers-and-product-profile-admins) — 产品配置文件管理员可以在[!DNL Adobe Admin Console]中管理产品的用户。

## 添加产品管理员

>[!BEGINTABS]

>[!NOTE]
>
>将产品管理员添加为产品管理员之前，请为其分配[用户角色](#add-users)。 基本Commerce权限需要用户角色。

>[!TAB GA（2025年10月13日之后配置）]

1. 导航到<https://adminconsole.adobe.com>并使用您的Adobe ID登录。

1. 选择您的组织。

1. 选择&#x200B;[!UICONTROL **用户**]&#x200B;选项卡。

1. 选择&#x200B;[!UICONTROL **管理员**]&#x200B;选项卡。

1. 单击&#x200B;[!UICONTROL **添加管理员**]。

1. 输入要添加为管理员的用户名或电子邮件地址，然后单击&#x200B;[!UICONTROL **下一步**]。

1. 选择&#x200B;[!UICONTROL **产品配置文件管理员**]&#x200B;角色。

1. 单击&#x200B;**+**&#x200B;添加产品。

1. 选择要将管理员添加到的现有Commerce Optimizer实例。 Commerce Optimizer实例使用以下格式： `Adobe Commerce - <instance-name> - ACO - <environment-type> - <tenant-id>`。

1. 选择产品配置文件。

1. 单击&#x200B;[!UICONTROL **应用**]。

1. 单击&#x200B;[!UICONTROL **保存**]。

>[!TAB 提前访问（2025年10月13日之前配置）]

1. 导航到<https://adminconsole.adobe.com>并使用您的Adobe ID登录。

1. 选择您的组织。

1. 在&#x200B;[!UICONTROL **产品**]&#x200B;选项卡的&#x200B;[!UICONTROL **产品和服务**]&#x200B;下，选择&#x200B;[!UICONTROL **Adobe Commerce - Commerce Cloud Manager**]&#x200B;产品。

   ![选择产品](/help/cloud-service/assets/backend.png){width="600" zoomable="yes"}

1. 选择&#x200B;[!UICONTROL **管理员**]&#x200B;选项卡。

1. 单击&#x200B;[!UICONTROL **添加管理员**]。

1. 输入要添加为管理员的用户名或电子邮件地址，然后单击&#x200B;[!UICONTROL **保存**]。

>[!ENDTABS]

## 添加用户

以下说明提供了有关如何将用户添加到[!DNL Commerce Cloud Manager]和Commerce Optimizer的信息。 [!DNL Commerce Cloud Manager]界面允许您创建和管理Commerce Optimizer实例。 所有用户（包括开发人员和管理员）都需要执行此流程。

>[!NOTE]
>
>只有产品管理员和系统管理员可以将用户和开发人员添加到Adobe Commerce Optimizer产品。

>[!BEGINTABS]

>[!TAB GA（2025年10月13日之后配置）]

1. 导航到<https://adminconsole.adobe.com>并使用您的Adobe ID登录。

1. 选择您的组织。

1. 选择&#x200B;[!UICONTROL **产品**]&#x200B;选项卡。

1. 选择&#x200B;[!UICONTROL **Adobe Commerce**]&#x200B;产品。

1. 如果要将用户添加到Commerce Cloud Manager界面(用户可以在该界面中创建和管理Commerce Optimizer实例)，请选择Manager产品，或者选择要将用户添加到的现有Commerce Optimizer实例。 Commerce Optimizer实例使用以下格式： `Adobe Commerce - <instance-name> - ACO - <environment-type> - <tenant-id>`。

1. 选择&#x200B;[!UICONTROL **用户**]&#x200B;选项卡，然后单击&#x200B;[!UICONTROL **添加用户**]。

1. 输入要添加的用户的用户名或电子邮件地址，然后单击&#x200B;[!UICONTROL **保存**]。

1. 选择所需的产品配置文件。

1. 单击&#x200B;[!UICONTROL **应用**]。

1. 单击&#x200B;[!UICONTROL **保存**]。

>[!TAB 提前访问（2025年10月13日之前配置）]

1. 导航到<https://adminconsole.adobe.com>并使用您的Adobe ID登录。

1. 选择您的组织。

1. 在&#x200B;[!UICONTROL **产品**]&#x200B;选项卡的&#x200B;[!UICONTROL **产品和服务**]&#x200B;下，选择&#x200B;[!UICONTROL **Adobe Commerce - Commerce Cloud Manager**]&#x200B;产品。

   ![选择产品](/help/cloud-service//assets/backend.png){width="600" zoomable="yes"}

1. 单击&#x200B;[!UICONTROL **默认 — Cloud Manager**]&#x200B;产品配置文件。

1. 选择&#x200B;[!UICONTROL **用户**]&#x200B;选项卡，然后单击&#x200B;[!UICONTROL **添加用户**]。

   ![选项卡选择](/help/cloud-service/assets/tab-select.png){width=600 zoomable="yes"}

1. 输入要添加的用户的用户名或电子邮件地址，然后单击&#x200B;[!UICONTROL **保存**]。

>[!ENDTABS]

### 添加开发人员和产品配置文件管理员

要添加开发人员和产品配置文件管理员，请重复[添加用户](#add-users)过程，但选择&#x200B;[!UICONTROL **开发人员**]&#x200B;或&#x200B;[!UICONTROL **管理员**]&#x200B;选项卡，而不是&#x200B;[!UICONTROL **用户**]&#x200B;选项卡。

>[!NOTE]
>
>在将开发人员添加为开发人员之前，为其分配用户角色。 基本Commerce权限需要用户角色。

![选项卡选择](/help//cloud-service/assets/tab-select.png){width=600 zoomable="yes"}

## 批量用户管理

您可以使用以下方法之一更高效地添加多个用户：

- 使用Adobe Admin Console中的&#x200B;**通过CSV添加用户**&#x200B;功能执行[批量CSV上传](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html){target="_blank"}。
- 通过创建[用户组](https://helpx.adobe.com/enterprise/using/user-groups.html){target="_blank"}将多个用户添加到角色。 然后，将&#x200B;[!UICONTROL **Adobe Commerce - Commerce Cloud Manager**]&#x200B;产品添加到用户组。

## 身份管理和单点登录配置

{{ims-identity-and-sso-config}}
