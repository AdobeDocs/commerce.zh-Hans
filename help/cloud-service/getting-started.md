---
title: 开始使用 [!DNL Adobe Commerce as a Cloud Service]
description: 了解如何使用 [!DNL Adobe Commerce as a Cloud Service]。
role: Admin, Developer, User
exl-id: 58d98b9e-b41d-44db-9666-c924a5b005b3
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目(Adobe管理的SaaS基础架构)。"
source-git-commit: 81dd617b0a6460b8dcb01c0a21b696663b0ae493
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# 快速入门

[!DNL Adobe Commerce as a Cloud Service]提供大部分现成的配置。 完成几个基本设置过程后，您的存储将很快启动并运行。 本指南将指导您完成创建和使用实例。

单击以下选项卡可查看以下用户类型的概要工作流概述：

* 管理员
* 商家
* 开发人员

>[!BEGINTABS]

>[!TAB 管理员和商家工作流]

此图表提供了管理员和商家如何访问和管理[!DNL Adobe Commerce as a Cloud Service]实例的简要概述。 有关管理员工作流的详细信息，请参阅[Adobe Admin Console指南](https://helpx.adobe.com/enterprise/admin-guide.html)。

![[!DNL Adobe Commerce as a Cloud Service]商家流程图](./assets/merchant-flow.svg){zoomable="yes"}

>[!TAB 开发人员工作流程]

此图提供了开发人员如何使用App Builder为[!DNL Adobe Commerce as a Cloud Service]创建集成的简要概述。 有关详细信息，请参阅[API文档](https://developer.adobe.com/commerce/webapi/rest/)。

![[!DNL Adobe Commerce as a Cloud Service]开发人员流程图](./assets/developer-flow.svg){zoomable="yes"}

>[!ENDTABS]

## 创建实例

>[!NOTE]
>
>在创建实例之前，贵组织的产品管理员或系统管理员必须将您添加为[!DNL Adobe Commerce as a Cloud Service]产品的用户。 有关详细信息，请参阅[添加用户和管理员](./user-management.md#add-users-and-admins)。

[!DNL Adobe Commerce as a Cloud Service]实例使用基于信用的系统。 您可以创建多个实例，但每个实例都需要相对数量的积分。 您最初的积分数量取决于您的订购。

1. 登录到您的[Adobe Experience Cloud](https://experience.adobe.com/)帐户。

1. 在[!UICONTROL Quick access]下，单击&#x200B;[!UICONTROL **Commerce**]&#x200B;以打开[!UICONTROL Commerce Cloud Manager]。

   [!UICONTROL Commerce Cloud Manager]显示您的Adobe IMS组织中可用的[!DNL Adobe Commerce as a Cloud Service]实例的列表。

1. 单击屏幕右上角的&#x200B;[!UICONTROL **添加实例**]。

   ![创建实例](./assets/create-instance.png){width="50%" align="center" zoomable="yes"}

1. 选择&#x200B;[!UICONTROL **Commerce as a Cloud Service**]。

1. 为您的实例输入&#x200B;**名称**&#x200B;和&#x200B;**描述**。

1. 选择要托管实例的地区。

   >[!NOTE]
   >
   >创建实例后，您将无法修改区域。

1. 为您的实例选择&#x200B;[!UICONTROL **环境类型**]。 您可以选择以下选项：

   * [!UICONTROL **沙盒**] — 非常适合用于设计和测试目的。 您应该使用沙盒环境开始[!DNL Adobe Commerce as a Cloud Service]历程。
   * [!UICONTROL **生产**] — 适用于实时商店和面向客户的网站。

   >[!NOTE]
   >
   >* 沙盒实例当前仅限于北美地区。
   >* 安装示例数据的选项当前不可用。

1. 单击&#x200B;[!UICONTROL **添加实例**]。

## 访问实例

创建实例后，您可以从[!UICONTROL Commerce Cloud Manager]访问它。

1. 登录到您的[Adobe Experience Cloud](https://experience.adobe.com/)帐户。

1. 在[!UICONTROL Quick access]下，单击&#x200B;[!UICONTROL **Commerce**]&#x200B;以打开[!UICONTROL Commerce Cloud Manager]。

   [!UICONTROL Commerce Cloud Manager]显示您的Adobe IMS组织中可用的实例列表。

1. 要打开某个实例的[!UICONTROL Commerce Admin]，请单击该实例名称。

>[!TIP]
>
>要查看有关实例的信息(包括REST和GraphQL端点以及管理员URL)，请单击实例名称旁边的信息图标。

## 导入您的目录

默认情况下，[!DNL Adobe Commerce as a Cloud Service]实例不包含任何产品数据。 在导入您自己的目录之前，为测试和学习目的创建实例时，您可以选择包含示例产品数据。

有两种方法可以将您的目录导入[!DNL Adobe Commerce as a Cloud Service]：

* [**Commerce管理员**](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/import/data-import) — 一个用户友好的界面，允许您通过单击几下导入目录数据。
* [**导入JSON API**](https://developer.adobe.com/commerce/webapi/rest/modules/import/#import-json-api) — 一个REST API，允许您以编程方式导入目录数据。

<!-- TODO

- Add guidance about how to choose which method to use
- Add guidance for new vs existing customers (cross-reference OR and _include file for migration content)

-->

## 设置店面

现在您已创建一个实例，可以继续[设置](storefront.md)由Edge Delivery Services提供支持的Commerce店面。
