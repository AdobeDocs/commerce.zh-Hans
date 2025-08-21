---
title: 将Commerce数据连接到Adobe Experience Platform
description: 了解如何将Commerce数据连接到Adobe Experience Platform。
feature: Personalization, Integration, Configuration
exl-id: 8ba33277-38a5-45af-86e0-906cfb3b998d
source-git-commit: 7c480598ebfb862432b0e83a27467e1d932c6666
workflow-type: tm+mt
source-wordcount: '2917'
ht-degree: 0%

---

# 将Commerce数据连接到Adobe Experience Platform

安装[!DNL Data Connection]扩展时，在Commerce **管理员**&#x200B;的&#x200B;**服务**&#x200B;下的&#x200B;_系统_&#x200B;菜单中会显示两个新的配置页面。

- Commerce服务连接器
- [!DNL Data Connection]

要将Adobe Commerce实例连接到Adobe Experience Platform，必须配置这两个连接器，从Commerce服务连接器开始，然后使用[!DNL Data Connection]扩展完成。

## 配置Commerce服务连接器

如果以前安装过Adobe Commerce服务，则您可能已配置Commerce服务连接器。 如果没有，则必须在[Commerce Services Connector](../landing/saas.md)页面上完成以下任务：

1. 登录到您的Commerce帐户以[检索您的生产和沙盒API密钥](../landing/saas.md#credentials)。
1. 选择[SaaS数据空间](../landing/saas.md#saas-configuration)。
1. 登录到您的Adobe帐户以[检索您的组织ID](../landing/saas.md#ims-organization-optional)。

配置Commerce Services连接器后，再配置[!DNL Data Connection]扩展。

## 配置[!DNL Data Connection]扩展

在本节中，您将了解如何配置[!DNL Data Connection]扩展。

### 添加服务帐户和凭据详细信息

如果您计划收集和发送[历史订单数据](#send-historical-order-data)或[客户配置文件数据](#send-customer-profile-data)，则必须添加服务帐户和凭据详细信息。 此外，如果您正在配置[Audience Activation](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html)扩展，则必须完成这些步骤。

如果您仅收集和发送店面或后台数据，则可以跳到[常规](#general)部分。

#### 步骤1：在Adobe Developer Console中创建项目

在Adobe Developer Console中创建一个验证Commerce的项目，以便它能进行Experience Platform API调用。

要创建项目，请按照[身份验证和访问Experience Platform API](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html)教程中所述的步骤进行操作。

在学习本教程时，请确保您的项目具备以下条件：

- 访问以下[产品配置文件](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html#select-product-profiles)： **默认的生产所有访问**&#x200B;和&#x200B;**AEP默认所有访问**。
- 已配置正确的[角色和权限](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html#assign-api-to-a-role)。
- 如果您决定使用JSON Web令牌(JWT)作为服务器到服务器的身份验证方法，则还必须上传私钥。

此步骤的结果将创建一个配置文件，供您在下一步中使用。

#### 步骤2：下载配置文件

下载[工作区配置文件](https://developer.adobe.com/commerce/extensibility/events/project-setup/#download-the-workspace-configuration-file)。 `<workspace-name>.json`文件包含您需要在Commerce管理员的&#x200B;**服务帐户/凭据详细信息**&#x200B;页面中输入的所有值。

![[!DNL Data Connection]管理员配置](./assets/epc-admin-config.png){width="700" zoomable="yes"}

1. 在Commerce管理员中，导航到&#x200B;**商店** >设置> **配置** > **服务** > **[!DNL Data Connection]**。

1. 从&#x200B;**Adobe Developer授权类型**&#x200B;菜单中选择您实施的服务器到服务器授权方法。 Adobe建议使用OAuth。 已弃用JWT。 [了解详情](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)。

1. （仅限JWT）将`private.key`文件的内容复制并粘贴到&#x200B;**客户端密钥**&#x200B;字段中。 使用以下命令复制内容。

   ```bash
   cat config/private.key | pbcopy
   ```

   有关[文件的详细信息，请参阅](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/)服务帐户(JWT)身份验证`private.key`。

1. 将`<workspace-name>.json`文件的内容复制到&#x200B;**服务帐户/凭据详细信息**&#x200B;字段，如`"client_id"`、`"client_secrets"`、`"technical_account_email"`、`"technical_account_id"`等。

1. 单击&#x200B;**保存配置**。

1. 单击&#x200B;**[!UICONTROL Test connection]**&#x200B;按钮以确保您输入的服务帐户和凭据信息正确。

### 常规

1. 在管理员中，转到&#x200B;**系统** >服务> **[!DNL Data Connection]**。

   ![[!DNL Data Connection]设置](./assets/epc-settings.png){width="700" zoomable="yes"}

1. 在&#x200B;**常规**&#x200B;下的&#x200B;**设置**&#x200B;选项卡中，验证与您的Adobe Experience Platform帐户关联的ID，该ID已在[Commerce Services Connector](../landing/saas.md#organizationid)中配置。 组织ID是全局的。 每个Adobe Commerce实例只能关联一个组织ID。

1. 在&#x200B;**范围**&#x200B;下拉列表中，将上下文设置为&#x200B;**网站**。

1. （可选）如果您已将[AEP Web SDK (alloy)](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)部署到您的网站，请启用该复选框并添加AEP Web SDK的名称。 否则，请将这些字段留空，[!DNL Data Connection]扩展将为您部署一个字段。

   >[!NOTE]
   >
   >如果您指定自己的AEP Web SDK，[!DNL Data Connection]扩展将使用与该SDK关联的数据流ID，而不是使用在此页面上指定的数据流ID（如果有）。

### 数据收集

在此部分中，您可以指定要收集并发送到Experience Platform Edge的数据类型。 有三种类型的数据：

- **行为** （客户端数据）是在店面中捕获的数据。 这包括购物者交互，如`View Page`、`View Product`、`Add to Cart`和[申请列表](events.md#b2b-events)信息（适用于B2B商家）。

- **后台** （服务器端数据）是Commerce服务器中捕获的数据。 这包括有关订单状态的信息，例如订单是否已下达、已取消、已退款、已发运或已完成。 它还包含[历史订单数据](#send-historical-order-data)。

- **配置文件**&#x200B;是与购物者的配置文件信息相关的数据。 了解[更多](#send-customer-profile-data)。

要确保Adobe Commerce实例可以开始数据收集，请查看[先决条件](overview.md#prerequisites)。

请参阅活动主题以了解有关[店面](events.md#storefront-events)、[后台](events-backoffice.md)和[配置文件](events-backoffice.md#customer-profile-events-server-side)事件的更多信息。

>[!NOTE]
>
>**数据收集**&#x200B;部分中的所有字段均适用于&#x200B;**网站**&#x200B;范围或更高版本。

1. 如果要发送店面行为数据，请选择&#x200B;**店面事件**。

1. 如果要发送订单状态信息（如订单已下达、已取消、已退款或已发货），请选择&#x200B;**后台事件**。

   >[!NOTE]
   >
   >如果选择&#x200B;**后台事件**，则所有后台数据都会发送到Experience Platform Edge。 如果购物者选择退出数据收集，您必须在Experience Platform中明确设置购物者的隐私偏好设置。 这与店面事件不同，店面事件收集器已根据购物者偏好处理同意。 了解[更多](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/consent/adobe/dataset.html)有关在Experience Platform中设置购物者的隐私首选项的信息。

1. (如果您使用自己的AEP Web SDK，请跳过此步骤。)[在Adobe Experience Platform中创建](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html#create)数据流，或选择要用于收集的现有数据流。 在&#x200B;**数据流ID**&#x200B;字段中输入该数据流ID。

1. 输入要包含Commerce数据的&#x200B;**数据集ID**。 要查找数据集ID，请执行以下操作：

   1. 打开Experience Platform UI，然后在左侧导航中选择&#x200B;**数据集**&#x200B;以打开&#x200B;**数据集**&#x200B;仪表板。 仪表板列出您组织的所有可用数据集。 将显示每个列出数据集的详细信息，包括其名称、数据集所遵循的架构以及最近一次摄取运行的状态。
   1. 打开与数据流关联的数据集。
   1. 在右侧窗格中，查看有关数据集的详细信息。 复制数据集ID。

1. 若要确保根据[cron](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/cron.html)作业按计划更新后台事件数据，必须将`Sales Orders Feed`索引更改为`Update by Schedule`。

   1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL System]** > _[!UICONTROL Tools]_>**[!UICONTROL Index Management]**。

   1. 选中`Sales Orders Feed`索引器的复选框。

   1. 将&#x200B;**[!UICONTROL Actions]**&#x200B;设置为`Update by Schedule`。

   1. 如果您是首次启用后台数据，请运行以下命令来重新索引并触发重新同步。 只要[cron](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/cron.html)作业设置正确，后续的重新同步就会自动进行。

      ```bash
      bin/magento index:reindex sales_order_data_exporter_v2
      ```

      ```bash
      bin/magento saas:resync --feed orders
      ```

#### 字段描述

| 字段 | 描述 |
|--- |--- |
| 范围 | 您希望应用配置设置的特定网站。 |
| 组织ID（全局） | 属于购买Adobe DX产品的组织的ID。 此ID可将您的Adobe Commerce实例链接到Adobe Experience Platform。 |
| AEP Web SDK是否已部署到您的站点 | 如果您已将自己的AEP Web SDK部署到网站，请选中此复选框 |
| AEP Web SDK名称（全局） | 如果您已将Experience Platform Web SDK部署到网站，请在此字段中指定该SDK的名称。 这允许Storefront事件收集器和店面事件SDK使用您的Experience Platform Web SDK，而不是[!DNL Data Connection]扩展部署的版本。 如果您没有将Experience Platform Web SDK部署到您的网站，请将此字段留空，然后[!DNL Data Connection]扩展会为您部署一个扩展。 |
| 店面活动 | 只要组织ID和数据流ID有效，默认情况下都会选中。 店面活动在购物者浏览您的网站时收集他们的匿名行为数据。 |
| 后台活动 | 如果选中，则事件有效负荷包含匿名的订单状态信息，例如订单是否已下达、取消、退款或发运。 |
| 数据流ID（网站） | 允许数据从Adobe Experience Platform流向其他Adobe DX产品的ID。 此ID必须关联到您的特定Adobe Commerce实例中的特定网站。 如果您指定自己的Experience Platform Web SDK，请不要在此字段中指定数据流ID。 [!DNL Data Connection]扩展使用与该SDK关联的数据流ID，并忽略在此字段中指定的任何数据流ID（如果有）。 |
| 数据集ID（网站） | 包含Commerce数据的数据集的ID。 除非您已取消选中&#x200B;**店面事件**&#x200B;或&#x200B;**后台事件**&#x200B;复选框，否则需要此字段。 此外，如果您使用的是自己的Experience Platform Web SDK，因此没有指定数据流ID，则仍必须添加与数据流关联的数据集ID。 否则，无法保存此表单。 |

完成新用户引导后，店面数据开始流入Experience Platform Edge。 后台数据大约需要5分钟才能显示在边缘。 根据cron时间表，可以在Edge看到后续更新。

### 发送客户个人资料数据

有两种类型的配置文件数据可发送到Experience Platform：配置文件记录和时间序列配置文件事件。

配置文件记录包含购物者在Commerce实例中创建配置文件时保存的数据，例如购物者的姓名。 如果您的架构和数据集配置正确[](profile-data.md)，则会将配置文件记录发送到Experience Platform并转发到Adobe的配置文件管理和分段服务： [Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html#)。

时间序列配置文件事件包含有关购物者配置文件信息的数据，例如，购物者在您的网站上创建、编辑或删除帐户的情况。 将配置文件事件数据发送到Experience Platform时，该数据会位于可供其他DX产品使用的数据集中。

1. 确保您已[提供](#add-service-account-and-credential-details)服务帐户和凭据详细信息。

1. 确保您为[配置文件记录数据摄取](profile-data.md)和[时间序列配置文件事件数据摄取](update-xdm.md#time-series-profile-event-data)指定了架构和数据集。

1. 如果要将配置文件数据发送到Experience Platform，请在&#x200B;**客户配置文件**&#x200B;复选框中放置复选标记。

1. 输入&#x200B;**配置文件数据集ID**。

   配置文件记录数据必须使用的数据集必须与您当前用于行为和后台事件数据的数据集不同。

1. 如果您不想通过用于行为数据和后台数据的相同数据流ID流式传输配置文件事件，请通过相同数据流ID **从**&#x200B;流式传输客户配置文件中删除复选标记，然后输入要改用的数据流ID。

配置文件记录在Real-Time CDP中可用大约需要10分钟。 配置文件事件会立即开始流式传输。

>[!TIP]
>
>如果您未在Experience Platform中看到配置文件数据，请参阅[Commerce知识库](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/data-connection-customer-profiles-not-exported)以获取故障排除建议。

#### 字段描述

| 字段 | 描述 |
|--- |--- |
| 客户配置文件 | 如果要收集并发送客户配置文件记录，请选中此复选框。 |
| 配置文件数据集ID | 配置文件记录必须使用与用于行为和后台事件的数据集不同的数据集。 |
| 通过相同的数据流ID流式传输客户用户档案 | 决定是否要使用当前用于行为和后台事件的相同数据流。 |
| 客户用户档案的数据流 | 指定特定于客户配置文件记录的数据流。 |

### 发送历史订单数据

Adobe Commerce最多收集5年的[历史订单数据和状态](events-backoffice.md#back-office-events)。 您可以使用[!DNL Data Connection]扩展将该历史数据发送到Experience Platform，以丰富客户配置文件并根据这些过去的订单个性化客户体验。 该数据存储在Experience Platform内的数据集中。

虽然Commerce已收集历史订单数据，但您必须完成多个步骤才能将该数据发送到Experience Platform。

观看本视频，了解有关历史订单的更多信息，然后完成以下步骤来实施历史订单收集。

>[!VIDEO](https://video.tv.adobe.com/v/3424672)

#### 设置订单同步服务

订单同步服务使用[消息队列框架](https://developer.adobe.com/commerce/php/development/components/message-queues/)和RabbitMQ。 完成这些步骤后，订单状态数据可以同步到SaaS，在发送到Experience Platform之前需要这样做。

1. 确保您已[提供](#add-service-account-and-credential-details)服务帐户和凭据详细信息。

1. [启用](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/service/rabbitmq.html) RabbitMQ。

   >[!NOTE]
   >
   >已为Commerce版本2.4.7及更高版本设置了RabbitMQ，但您必须启用消费者。

1. 使用`.magento.env.yaml`环境变量在`CRON_CONSUMERS_RUNNER`中通过cron作业启用消息队列使用者。

   ```yaml
      stage:
        deploy:
          CRON_CONSUMERS_RUNNER:
            cron_run: true
   ```

   >[!NOTE]
   >
   >请参阅[部署变量文档](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-deploy.html#cron_consumers_runner)以了解所有可用的配置选项。

启用订单同步服务后，您可以在&#x200B;**[!UICONTROL [!DNL Data Connection]]**&#x200B;页面中指定历史订单日期范围。

#### 指定订单历史记录日期范围

指定要发送到Experience Platform的历史订单的日期范围。

1. 在管理员中，转到&#x200B;**系统** >服务> **[!DNL Data Connection]**。

1. 选择&#x200B;**订单历史记录**&#x200B;选项卡。

   ![[!DNL Data Connection]订单历史记录](./assets/epc-order-history.png){width="700" zoomable="yes"}

1. 在&#x200B;**订单历史记录同步**&#x200B;下，**从设置复制数据集ID**&#x200B;复选框已启用。 这将确保您使用在&#x200B;**设置**&#x200B;选项卡中指定的相同数据集。

1. 在&#x200B;**从**&#x200B;和&#x200B;**到**&#x200B;字段中，指定要发送的历史订单数据的日期范围。 您不能选择超过五年的日期范围。

1. 选择&#x200B;**[!UICONTROL Start Sync]**&#x200B;以触发同步开始。 历史订单数据是批处理数据，而不是店面和后台的流数据。 批量数据大约需要45分钟才能到达Experience Platform。

##### 字段描述

| 字段 | 描述 |
|--- |--- |
| 从设置中复制数据集ID | 复制您在&#x200B;**设置**&#x200B;选项卡中输入的数据集ID。 |
| 数据集ID（网站） | 包含Commerce数据的数据集的ID。 除非您已取消选中&#x200B;**店面事件**&#x200B;或&#x200B;**后台事件**&#x200B;复选框，否则需要此字段。 此外，如果您使用的是自己的Experience Platform Web SDK，因此没有指定数据流ID，则仍必须添加与数据流关联的数据集ID。 否则，无法保存此表单。 |
| 从 | 您要开始收集订单历史记录数据的起始日期。 |
| 至 | 您要结束收集订单历史记录数据的起始日期。 |
| 开始同步 | 开始将订单历史记录数据同步到Experience Platform Edge的过程。 如果&#x200B;**[!UICONTROL Dataset ID]**&#x200B;字段为空或数据集ID无效，则此按钮被禁用。 |

### 数据自定义

在&#x200B;**数据自定义**&#x200B;选项卡上，您可以查看在[!DNL Commerce]中配置并发送到Experience Platform的任何自定义属性。

![[!DNL Data Connection]数据自定义](./assets/epc-data-customization.png){width="700" zoomable="yes"}

>[!IMPORTANT]
>
>确保您在[数据收集](#data-collection)选项卡上指定的&#x200B;**数据流ID**&#x200B;与链接到架构的ID匹配，以便摄取自定义属性。

为订单创建自定义属性并将它们发送到Experience Platform时，Commerce中的属性名称必须与Experience Platform上[!DNL Commerce]架构中的属性名称匹配。 如果两者不匹配，则可能很难识别差异。 如果您的名称不匹配，**自定义订单属性**&#x200B;表可以帮助解决此问题。

**自定义订单属性**&#x200B;表提供了在Experience Platform中的[!DNL Commerce]后台和[!DNL Commerce]架构之间自定义订单属性的配置和映射的可见性。 此表允许您查看跨不同来源的订单层和订单项目层自定义属性，从而更容易识别缺少或未对齐的属性。 它还显示数据集ID以帮助区分实时数据集和历史数据集，因为每个数据集可以具有自己的自定义属性。

如果在表中的自定义属性名称旁边没有出现绿色复选标记，则表示源中的属性名称不匹配。 在一个源中更正属性名称，将出现绿色复选标记，指示名称现在匹配。

- 如果在Experience Platform的架构中更新了属性名称，则必须在&#x200B;**数据自定义**&#x200B;选项卡上保存配置以触发Experience Platform架构更改。 单击&#x200B;**按钮时，此更改将反映在**&#x200B;自定义订单属性&#x200B;**[!UICONTROL Refresh]**&#x200B;表中。
- 如果属性名称在[!DNL Commerce]中更新，则必须生成订单事件以更新&#x200B;**自定义订单属性**&#x200B;表中的名称。 此更改将在大约60分钟后反映出来。

详细了解如何[设置自定义属性](custom-attributes.md)。

#### 字段描述

| 字段 | 描述 |
|--- |--- |
| 数据集 | 显示包含自定义属性的数据集。 实时数据集和历史数据集可以拥有自己的自定义属性。 |
| Adobe Commerce | 显示在[!DNL Commerce]后台创建的任何自定义属性。 |
| Experience Platform | 显示在Experience Platform的[!DNL Commerce]架构中指定的任何自定义属性。 |
| 刷新 | 从Experience Platform中的[!DNL Commerce]架构检索任何自定义属性名称。 |

## 确认已收集事件数据

要确认正在从Commerce存储中收集数据，请使用[Adobe Experience Platform Debugger](https://experienceleague.adobe.com/docs/experience-platform/debugger/home.html)来检查您的Commerce网站。 确认正在收集数据后，通过运行返回来自您创建的[数据集的数据](overview.md#prerequisites)的查询，可以验证店面和后台事件数据是否显示在边缘。

1. 在Experience Platform的左侧导航中选择&#x200B;**查询**，然后单击[!UICONTROL Create Query]。

   ![查询编辑器](assets/query-editor.png)

1. 当查询编辑器打开时，输入从数据集选择数据的查询。

   ![创建查询](assets/create-query.png)

   例如，您的查询可能如下所示：

   ```sql
   SELECT * from `your_dataset_name` ORDER by TIMESTAMP DESC
   ```

1. 查询运行后，结果将显示在&#x200B;**控制台**&#x200B;选项卡旁边的&#x200B;**结果**&#x200B;选项卡中。 此视图显示查询的表格输出。

   ![查询编辑器](assets/query-results.png)

在此示例中，您看到来自`commerce.productListAdds`、`commerce.productViews`、`web.webpagedetails.pageViews`等的事件数据。 通过此视图，可验证您的Commerce数据是否已到达边缘。

如果结果不符合预期，请打开您的数据集并查找任何失败的批量导入。 了解有关[批处理导入疑难解答的详细信息](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/troubleshooting.html)。

### 验证配置文件数据是否显示在Experience Platform中

如果您未在Experience Platform中看到配置文件数据，请参阅[Commerce知识库](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/data-connection-customer-profiles-not-exported)以获取故障排除建议。

## 后续步骤

在将Commerce数据发送到Experience Platform Edge时，其他Adobe Experience Cloud产品(如Adobe Journey Optimizer)可以使用该数据。 例如，您可以将Journey Optimizer配置为侦听某些事件，并根据该事件数据触发针对首次用户或存在放弃购物车的电子邮件。 了解如何通过在Journey Optimizer中[创建客户历程](using-ajo.md)来扩展Commerce平台。
