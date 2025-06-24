---
title: 快速入门
description: 了解如何使用 [!DNL Adobe Commerce Optimizer]。
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目(Adobe管理的SaaS基础架构)。"
source-git-commit: f49a86b8793e2d91413acfbc0b922cb94db67362
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 0%

---

# 开始使用

本文向您介绍如何快速掌握[!DNL Adobe Commerce Optimizer]。 虽然本指南重点介绍推销商和管理员角色，但其中确实包括开发人员将执行的简短高级任务。 有关特定于开发人员的详细内容，请参阅[开发人员文档](https://developer-stage.adobe.com/commerce/services/composable-catalog/)。

## 你的角色是什么？

成功设置[!DNL Adobe Commerce Optimizer]通常涉及以下团队成员：

- 管理员
- 开发人员
- 推销员

每个团队成员都有自己的一组角色和职责，如下表所述：

| 角色 | 任务 |
|---|---|
| 管理员 | 使用Admin Console创建管理员、用户组、用户和开发人员&#x200B;。 |
|  | 在Commerce Cloud Manager中创建新的[!DNL Adobe Commerce Optimizer]实例&#x200B;。 |
|  | 设置策略和目录视图。 |
| 开发人员 | 使用Developer Console创建项目、授予开发人员API访问权限，以及安装所需的应用程序和自定义设置。 |
|  | 使用API Mesh和App Builder连接到您的后台系统（购物车、结账）&#x200B;。 |
|  | 使用Merchandising Services数据摄取API从现有商务解决方案中摄取目录数据&#x200B;。 |
|  | 设置您的店面 |
| 推销员 | 设置产品发现&#x200B;。 |
|  | 设置产品推荐。 |

每个角色都在[!DNL Adobe Commerce Optimizer]环境的成功载入和启动中起着不可或缺的作用。 下图显示了组织中每个角色从高层次开始到完成的工作流：

![高级工作流](./assets/high-level-workflow.png){zoomable="yes"}

### 管理员

管理员负责设置实例，管理组织的用户、组和权限。

- **[访问Adobe Admin Console](https://helpx.adobe.com/enterprise/admin-guide.html)** — 管理整个组织的Adobe权限。 请参阅[用户管理](./user-management.md)，了解您或您组织的产品管理员或系统管理员如何将用户添加到[!DNL Adobe Commerce Optimizer]产品。

- **创建实例** - [!DNL Adobe Commerce Optimizer]实例使用基于信用的系统。 您可以创建多个沙盒和生产实例，每个实例都需要一个相应的点数。 您最初的积分数量取决于您的订购。 [了解详情](#create-an-instance)。

- **访问实例** — 创建实例后，您可以从[!UICONTROL Commerce Cloud Manager]访问它。 [了解详情](#access-an-instance)。

- **设置目录视图和策略** — 了解如何[定义您的目录视图和策略](./setup/catalog-view.md)。 目录不仅包含您的产品数据，还有助于您定义业务结构。

### 开发人员

开发人员可创建项目和凭据、安装扩展、摄取目录数据以及执行一般平台架构任务。 有关特定于开发人员的详细内容，请参阅[开发人员文档](https://developer-stage.adobe.com/commerce/services/composable-catalog/)。

- **访问Developer Console** — 访问[Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started)以为[!DNL Adobe Commerce Optimizer]创建项目、生成访问令牌并安装所需的应用程序和自定义项。

- **摄取目录数据** — 请参阅[数据摄取API](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/using-the-api/)文档，了解如何将目录数据导入[!DNL Adobe Commerce Optimizer]。

  所摄取的目录数据在[数据同步](./setup/data-sync.md)页面中可见。

- **设置店面** — 在设置店面之前，必须首先创建一个实例，该任务通常由组织的[管理员](#administrator)执行。 创建实例后，您就可以继续[设置](./storefront.md)由Edge Delivery Services支持的Commerce店面。

### 推销员

该商家使用购物者数据和分析功能来做出有关店面产品投放、定价和促销的战略决策，同时还可以通过产品发现和推荐来优化购物体验。

- **设置产品发现和推荐** — 了解如何通过产品发现和推荐，为购物者[创建个性化体验](./merchandising/overview.md)。

## 创建实例

1. 登录到您的[Adobe Experience Cloud](https://experience.adobe.com/)帐户。

1. 在[!UICONTROL Quick access]下，单击&#x200B;[!UICONTROL **Commerce**]&#x200B;以打开[!UICONTROL Commerce Cloud Manager]。

   [!UICONTROL Commerce Cloud Manager]显示您的Adobe IMS组织中可用的[!DNL Adobe Commerce]实例的列表，包括为[!DNL Adobe Commerce Optimizer]和[!DNL Adobe Commerce as a Cloud Service]配置的实例。

1. 单击屏幕右上角的&#x200B;[!UICONTROL **添加实例**]。

   ![创建实例](./assets/create-aco-instance.png){width="100%" align="center" zoomable="yes"}

1. 选择&#x200B;[!UICONTROL **Commerce Optimizer**]。

1. 为您的实例输入&#x200B;**名称**&#x200B;和&#x200B;**描述**。

1. 选择要托管实例的地区。

   >[!NOTE]
   >
   >创建实例后，无法更改区域。

1. 为您的实例选择以下&#x200B;[!UICONTROL **环境类型**]&#x200B;之一：

   - [!UICONTROL **沙盒**] — 非常适合用于设计和测试目的。 您应该使用沙盒环境开始[!DNL Adobe Commerce Optimizer]历程。
   - [!UICONTROL **生产**] — 适用于实时商店和面向客户的网站。

   >[!NOTE]
   >
   >沙盒实例当前仅限于北美地区。

1. 单击&#x200B;[!UICONTROL **添加实例**]。

   新实例现在可在Cloud Manager中使用。

1. 要查看实例详细信息(包括GraphQL和目录服务端点、访问Adobe Commerce Optimizer应用程序的URL以及实例ID（租户ID）)，请单击实例名称旁边的信息图标。

   ![创建实例](./assets/aco-instance-details.png){width="100%" align="center" zoomable="yes"}

## 访问实例

1. 登录到您的[Adobe Experience Cloud](https://experience.adobe.com/)帐户。

1. 在[!UICONTROL Quick access]下，单击&#x200B;[!UICONTROL **Commerce**]&#x200B;以打开[!UICONTROL Commerce Cloud Manager]。

   [!UICONTROL Commerce Cloud Manager]显示您的Adobe IMS组织中可用的实例列表。

1. 要打开与实例关联的[!UICONTROL Commerce Optimizer]应用程序，请单击实例名称。


