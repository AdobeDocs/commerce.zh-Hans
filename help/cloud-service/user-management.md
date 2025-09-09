---
title: 用户管理
description: 了解如何管理 [!DNL Adobe Commerce as a Cloud Service]中的用户。
exl-id: 9bc80fe6-6dfd-4bb3-8dc5-d5efd8a8d90c
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目(Adobe管理的SaaS基础架构)。"
role: Admin
source-git-commit: 492a22cd1fd8a63d3f4e55a3ddb81621439b624b
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 0%

---

# 用户管理

如果您希望用户在[!DNL Adobe Commerce as a Cloud Service]中访问管理员，您需要将他们添加为您的组织中的用户，并确保他们有权在[Adobe Admin Console](https://adminconsole.adobe.com){target="_blank"}中访问Cloud Service产品。

此进程需要具有[!DNL Adobe Commerce as a Cloud Service]访问权限的IMS组织。 只有组织的系统管理员或产品管理员可以执行这些流程。

>[!TIP]
>
>要同时添加多个用户，您可以执行[批量CSV上传](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html){target="_blank"}。
> 
> 您还可以通过创建[用户组](https://helpx.adobe.com/enterprise/using/user-groups.html){target="_blank"}将多个用户添加到角色。 然后，您可以将&#x200B;[!UICONTROL **Adobe Commerce - Commerce Cloud Manager**]&#x200B;产品添加到用户组。

## 了解角色

以下角色可用于[!DNL Adobe Commerce as a Cloud Service]。 要查看或编辑这些角色，请在Commerce管理员中导航到&#x200B;**系统** > **权限** > **用户角色**。

* **用户** — 用户对Commerce管理员具有管理员访问权限，但无法在Admin Console中管理产品级访问权限。 用户还可以使用积分在[中](./getting-started.md#create-an-instance)创建实例[!DNL Commerce Cloud Manager]。

* [**开发人员**](https://helpx.adobe.com/enterprise/using/manage-developers.html#Adddevelopers){target="_blank"}开发人员具有用户权限，并作为开发人员用户添加到Commerce实例。 这意味着他们可以使用[Admin UI SDK](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/){target="_blank"}、[配置事件](https://developer.adobe.com/commerce/extensibility/events/){target="_blank"}和[创建Webhook](https://developer.adobe.com/commerce/extensibility/webhooks/){target="_blank"}。

* 管理员 — 管理员分为三种类型：
   * [系统管理员](https://helpx.adobe.com/enterprise/using/admin-roles.html){target="_blank"} — 系统管理员可以通过Admin Console访问组织中的所有产品和产品配置文件。
   * [产品管理员](#add-a-product-admin) — 产品管理员可以在[中](#add-users-and-admins)管理产品的用户、角色和权限[!DNL Adobe Admin Console]，在Commerce管理员中[管理用户](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/user-accounts/permissions-users-all#create-a-user){target="_blank"}。
   * [产品配置文件管理员](#add-users-developers-and-product-profile-admins) — 产品配置文件管理员无权访问Adobe Commerce管理员，但可以在[!DNL Adobe Admin Console]中管理产品的用户。

有关授予Adobe Commerce中每个角色的权限的详细信息，请参阅[用户权限](#user-permissions)。

## 添加产品管理员

1. 导航到https://adminconsole.adobe.com并使用您的Adobe ID登录。

1. 选择您的组织。

1. 在&#x200B;[!UICONTROL **产品**]&#x200B;选项卡的&#x200B;[!UICONTROL **产品和服务**]&#x200B;下，选择&#x200B;[!UICONTROL **Adobe Commerce - Commerce Cloud Manager**]&#x200B;产品。

   ![选择产品](./assets/backend.png){width="600" zoomable="yes"}

1. 选择&#x200B;[!UICONTROL **管理员**]&#x200B;选项卡。

1. 单击&#x200B;[!UICONTROL **添加管理员**]。

1. 输入要添加为管理员的用户名或电子邮件地址，然后单击&#x200B;[!UICONTROL **保存**]。

## 添加用户、开发人员和产品配置文件管理员

以下说明提供了有关如何将用户和开发人员添加到[!DNL Commerce Cloud Manager]和Commerce管理员的信息。 [!DNL Commerce Cloud Manager]界面允许您创建和管理Commerce实例。

>[!NOTE]
>
>只有产品管理员和系统管理员可以将用户和开发人员添加到Adobe Commerce as a Cloud Service产品。

1. 导航到https://adminconsole.adobe.com并使用您的Adobe ID登录。

1. 选择您的组织。

1. 在&#x200B;[!UICONTROL **产品**]&#x200B;选项卡的&#x200B;[!UICONTROL **产品和服务**]&#x200B;下，选择&#x200B;[!UICONTROL **Adobe Commerce - Commerce Cloud Manager**]&#x200B;产品。

   ![选择产品](./assets/backend.png){width="600" zoomable="yes"}

1. 单击&#x200B;[!UICONTROL **默认 — Cloud Manager**]&#x200B;产品配置文件。

1. 选择&#x200B;[!UICONTROL **用户**]、[!UICONTROL **开发人员**]&#x200B;或&#x200B;[!UICONTROL **管理员**]&#x200B;选项卡，然后单击&#x200B;[!UICONTROL **添加用户**]、[!UICONTROL **添加开发人员**]&#x200B;或&#x200B;[!UICONTROL **添加管理员**]。

   >[!NOTE]
   >
   >从此屏幕添加的管理员是[产品配置文件管理员](#understanding-roles)，无权访问Commerce管理员。

   ![选项卡选择](./assets/tab-select.png){width=600 zoomable="yes"}

1. 输入要添加为管理员的用户名或电子邮件地址，然后单击&#x200B;[!UICONTROL **保存**]。

## 角色资源

下表描述了默认角色有权在Adobe Commerce管理员内部访问的资源。 要编辑每个角色的默认权限，请在Commerce管理员中导航到&#x200B;**系统** > **权限** > **用户角色**。

**用户**

* 目录
   * 库存
      * 产品
         * 读取产品价格

**开发人员**

* 目录
   * 库存
      * 产品
         * 读取产品价格
* 系统
   * 数据传输
      * 导入历史记录
* Adobe IO事件配置
   * 配置检查
   * 创建事件提供程序
   * 配置更新
   * 同步事件
   * 获取事件提供程序列表
* 事件框架
   * 事件列表
   * 测试事件连接
   * 订阅事件
   * 取消订阅事件
   * 事件状态
   * 用于获取事件订阅的API
   * 查看事件订阅管理UI
   * 创建事件订阅管理UI
   * 请求新的事件管理员UI
* Webhooks
   * Webhooks数字签名
      * Webhooks数字签名设置
      * Webhooks数字签名生成密钥
   * Webhooks管理
      * Webhooks网格
      * Webhooks编辑
      * 测试Webhook
      * API订阅webhook
      * 从webhook取消订阅API
      * Webhooks列表
      * 请求新Webhook
      * Webhooks日志
      * 获取Webhook列表

**管理员**

管理员有权访问所有权限。

## 将用户添加到AEM Assets或产品可视化图表

[!DNL Adobe Experience Manager Assets]和[!DNL Product Visuals powered by AEM Assets]用户需要以下设置。

如果您的帐户有权访问[Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service)，并且您希望允许用户同时访问[AEM Assets](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/overview){target="_blank"}和[!DNL Adobe Commerce as a Cloud Service]的高级功能，请使用以下流程：

>[!NOTE]
>
>没有适当资产权限的用户将无法访问[!DNL AEM Assets]的高级功能，例如[AI图像生成](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/generative-ai/generative-ai-in-aem){target="_blank"}、[生成的变量](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/generative-ai/generate-variations-integrated-editor){target="_blank"}等。

>[!TIP]
>
>要同时添加多个用户，您可以执行[批量CSV上传](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html){target="_blank"}。
>
>您还可以通过创建[用户组](https://helpx.adobe.com/enterprise/using/user-groups.html){target="_blank"}将多个用户添加到角色。 然后，您可以将&#x200B;[!UICONTROL **Adobe Experience Manager as a Cloud Service - Cloud Manager**]&#x200B;产品添加到用户组。

1. 导航到https://adminconsole.adobe.com并使用您的Adobe ID登录。

1. 选择您的组织。

1. 在&#x200B;[!UICONTROL **产品**]&#x200B;选项卡的&#x200B;[!UICONTROL **产品和服务**]&#x200B;下，选择&#x200B;[!UICONTROL **Adobe Experience Manager as a Cloud Service - Cloud Manager**]&#x200B;产品。

   ![选择产品](./assets/backend-aem.png){width="600" zoomable="yes"}

1. 选择&#x200B;[!UICONTROL **用户**]&#x200B;选项卡。

1. 单击&#x200B;[!UICONTROL **添加用户**]。

1. 输入要添加的用户的用户名或电子邮件地址。

1. 单击&#x200B;[!UICONTROL **添加产品**]。

1. 选择将AEM Assets与Commerce集成所需的以下产品配置文件：

   * 业务负责人 — 创建和管理项目所需。
   * 部署管理员 — 将代码从存储库部署到AEM时需要此项。

   如果您添加的开发人员不需要访问Cloud Manager或Experience Manager界面，您可以为他们分配开发人员角色。

   >[!NOTE]
   >
   >有关这些权限如何影响您访问AEM Assets的更多信息，请参阅[Cloud Manager产品配置文件](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/concepts/aem-cs-team-product-profiles#cloud-manager-product-profiles){target="_blank"}。

1. 单击&#x200B;[!UICONTROL **应用**]。

1. 单击&#x200B;[!UICONTROL **保存**]。

要确认用户具有访问权限，请单击用户的名称以打开其配置文件页面。 在&#x200B;[!UICONTROL **Products**]&#x200B;部分中，[!UICONTROL **Adobe Experience Manager as a Cloud Service - Cloud Manager**]&#x200B;产品下的&#x200B;[!UICONTROL **Completed**]&#x200B;应该为。 添加用户后，可能需要几秒钟才能看到其配置文件上的状态更新。 刷新页面可查看已更新的状态。

![产品访问权限](./assets/product-access.png){width="600" zoomable="yes"}

## 访问Experience Manager界面

将用户添加到AEM Assets后，他们可以通过导航到[!DNL Experience Manager]https://experience.adobe.com/[来访问](https://experience.adobe.com/){target="_blank"}界面。

1. 在&#x200B;[!UICONTROL **快速访问**]&#x200B;部分中，单击&#x200B;[!UICONTROL **Experience Manager**]，如果没有看到&#x200B;[!UICONTROL **Experience Manager**]，请单击&#x200B;[!UICONTROL **查看全部**]。 然后单击&#x200B;[!UICONTROL **Cloud Manager**]&#x200B;或直接导航到[https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}。

1. 从&#x200B;[!UICONTROL **Cloud Manager**]&#x200B;页面，单击&#x200B;[!UICONTROL **添加程序**]&#x200B;以开始。

1. [创建新程序](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/create-program){target="_blank"}。

1. [创建新环境](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/screens-as-cloud-service/onboarding-screens-cloud/creating-an-environment){target="_blank"}。

1. 创建环境后，返回到[Admin Console](https://adminconsole.adobe.com){target="_blank"}并选择&#x200B;[!UICONTROL **Adobe Experience Manager as a Cloud Service**]。

1. 您现在应该会看到新的产品配置文件。 选择包含`- author -`的。 例如，`<environment-name> - author - <program-id> - <environment-id>`。

1. [将用户添加到产品配置文件](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/requirements/users-and-roles){target="_blank"}。

* [配置AEM Assets以支持Commerce元数据](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/configure-aem)
* [将AEM Assets与Commerce集成以进行资源同步](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/setup-synchronization)
