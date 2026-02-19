---
title: 配置集成
description: 了解如何将Adobe Commerce项目与Experience Manager Assets项目连接起来，以便在这两个系统之间启用资源同步。
feature: CMS, Media
exl-id: 3533d010-926f-4d78-935c-98a9b7040d27
source-git-commit: d59c9d179018318d7a0ab1685d8e9e172eefa3ed
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 0%

---

# 配置集成

通过将Commerce连接到AEM Assets实例并选择资源同步的匹配策略来配置集成。

识别AEM Assets项目后，选择用于在Adobe Commerce和AEM Assets之间同步资产的匹配规则。

* **[!UICONTROL Match by product SKU]** — 将资源元数据中的SKU与[Commerce产品SKU](https://experienceleague.adobe.com/zh-hans/docs/commerce-operations/implementation-playbook/glossary#sku)匹配的默认规则，以确保资源与正确的产品关联。

* **[!UICONTROL Custom match]** — 匹配规则，用于需要自定义匹配逻辑的更复杂方案或特定业务要求。 实施自定义匹配需要在Adobe Developer App Builder中开发自定义代码以定义资源与产品的匹配方式。 更多详细信息即将推出……

对于初始设置，使用默认的&#x200B;*按产品SKU匹配*&#x200B;规则。

## 要求

在配置AEM Assets集成之前，请验证您已完成以下步骤：

* [配置AEM Assets项目](configure-aem.md)

* [!BADGE 仅限PaaS]{type=Informative tooltip="仅适用于云项目上的Adobe Commerce(Adobe管理的PaaS基础架构)。"} [安装Adobe Commerce包](configure-commerce.md)以添加扩展并生成使用该扩展所需的凭据和连接。

### IMS和用户权限

要使用资源选择器并在Commerce中提供更顺畅的设置，需要以下权限：

>[!BEGINTABS]

>[!TAB ACCS]

仅[!BADGE SaaS]{type=Positive tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目(Adobe管理的SaaS基础架构)。"}

默认情况下启用IMS身份验证。 将用户添加到&#x200B;**Adobe Admin Console**&#x200B;中的[AEM Assets DM OpenAPI Users - delivery](https://adminconsole.adobe.com/)产品配置文件以授予对AEM Assets交付层的访问权限。

用于Admin Console投放的![AEM Assets产品配置文件](../assets/aem-assets-delivery-product-profile.png){width="600" zoomable="yes"}

>[!TAB PaaS]

仅[!BADGE PaaS]{type=Informative tooltip="仅适用于云项目上的Adobe Commerce(Adobe管理的PaaS基础架构)。"}

1. [按照](https://experienceleague.adobe.com/docs/commerce-admin/start/admin/ims/adobe-ims-config.html?lang=zh-Hans){target=_blank}Commerce管理员指南&#x200B;*中的说明为Commerce*&#x200B;启用Adobe IMS。

1. [打开支持票证](https://experienceleague.adobe.com/zh-hans/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#support-cases)以请求资产选择器的自定义IMS客户端ID。

1. 将用户添加到&#x200B;**Adobe Admin Console**&#x200B;中的[AEM Assets DM OpenAPI Users - delivery](https://adminconsole.adobe.com/)产品配置文件以授予对AEM Assets交付层的访问权限。

>[!ENDTABS]

## 配置连接

1. 从Commerce管理员中，打开AEM Assets集成配置。

   1. 转到&#x200B;**[!UICONTROL Store]** >配置> **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**。

      ![AEM Assets集成启用该集成](../assets/aem-assets-view.png){width="600" zoomable="yes"}

>[!INFO]
>
> AEM Assets集成仅支持全局（默认）范围内的配置。 不支持网站级别的配置。 当您尝试在网站级别配置集成时，系统会忽略网站级别的设置，而使用全局配置值。

1. 仅[!BADGE PaaS]{type=Informative tooltip="仅适用于云项目上的Adobe Commerce(Adobe管理的PaaS基础架构)。"}输入&#x200B;**[!UICONTROL Asset Selector IMS Client ID]**。

   要启用资产选择器并自动填充“项目ID”和“环境ID”字段，需要使用此ID。 请参阅[IMS和用户权限](#ims-and-user-permissions)以获取此ID。 有关资产选择器的详细信息，请参阅[手动选择资产](../synchronize/asset-selector-integration.md)。

1. 从下拉菜单中选择AEM Assets环境&#x200B;**[!UICONTROL Program ID]**&#x200B;和&#x200B;**[!UICONTROL Environment ID]**。

   下拉列表会根据用户的IMS会话自动填充。 要使用此功能，请确保您拥有正确的[IMS和用户权限](#ims-and-user-permissions)。

   如果下拉列表不可用，您可以从AEM Cloud Manager URL手动输入ID： `https://author-p[Program ID]-e[EnvironmentID].adobeaemcloud.com/`

   通过从&#x200B;*[!UICONTROL Use system value]*&#x200B;中删除所选内容来编辑配置值。

1. [!BADGE 仅限PaaS]{type=Informative tooltip="仅适用于云项目上的Adobe Commerce(Adobe管理的PaaS基础架构)。"}选择[[!UICONTROL Commerce integration]](configure-commerce.md#add-the-integration-to-the-commerce-environment)以在Commerce和资源匹配服务之间验证请求。

1. 将&#x200B;**[!UICONTROL Synchronization enabled]**&#x200B;设置为`Yes`以允许Commerce接受来自AEM Assets的传入更新。

   启用集成后，可以使用其他配置选项来指定资源匹配条件。

1. 从&#x200B;**[!UICONTROL Asset matching rule]**&#x200B;下拉列表中选择一个资源匹配规则以进行资源同步。

   * 为&#x200B;**[!UICONTROL Match by SKU]**&#x200B;默认自动匹配[选择](../synchronize/default-match.md)，
   * 为&#x200B;**[!UICONTROL Custom match]**&#x200B;自定义自动匹配[选择](../synchronize/custom-match.md)(需要[Adobe Developer App Builder](https://experienceleague.adobe.com/zh-hans/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder)。)

1. 将为AEM Assets产品SKU定义的[Commerce元数据字段名称](configure-aem.md#configure-metadata)添加到&#x200B;**[!UICONTROL Match by product SKU attribute name]**&#x200B;字段`commerce:skus`中（默认情况下）。

1. 选择&#x200B;**[!UICONTROL Save Config]**&#x200B;以应用更新并启动资产同步。

   配置更新会触发初始同步过程，从而允许Commerce接受来自AEM Assets的传入更新。 同步所需的时间取决于资产量和特定配置。 该集成利用自动化流程来最大限度地减少同步所需的时间。

### 同步SLA

该集成保证了以下同步性能级别：

* `< 5 minutes for 99% of updates`

* `< 30 minutes for 99.9% of updates`

这可确保产品页面始终显示最新的图像，从而保持店面内容的准确且美观。

### 配置可视化图表所有者

**可视化所有者**&#x200B;设置确定在集成中提供产品图像的系统：

* Adobe Commerce — 使用在Commerce中托管的图像。

* AEM Assets — 使用从AEM同步的图像。

管理员显示该所有者的可用图像，而其余图像则呈灰显状态，并带有&#x200B;**hidden**&#x200B;标签。

有关图像显示行为的详细信息，请参阅[设置图像详细信息](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/catalog/products/digital-assets/product-image#set-image-details){target=_blank}主题。

>[!TIP]
>
> 从Commerce迁移到AEM Assets期间，请将&#x200B;**可视化所有者**&#x200B;设置为Commerce以避免图像链接损坏。 成功与AEM Assets同步所有产品后，切换到AEM Assets所有者以完成过渡。 这可以确保映像在整个过程中持续可用。

1. 导航到&#x200B;**[!UICONTROL Store]** >配置> **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**。

   ![AEM Assets集成可视化所有者功能](../assets/visualization-owner-detail.png){width="400" zoomable="yes"}

1. 选择&#x200B;**可视化所有者**&#x200B;源以显示图像。

1. 单击&#x200B;**[!UICONTROL Save Config]**&#x200B;以应用更新并启动资产同步。

### 可选。 配置自定义域URL

如果已为AEM Assets as a Cloud Service项目配置了[自定义域名](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name){target=_blank}，则必须将该域名添加到Commerce存储配置，以便Commerce的AEM Assets集成可以使用该域名。

1. 导航到&#x200B;**[!UICONTROL Store]** >配置> **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**。

   ![AEM Assets集成启用该集成](../assets/aem-assets-view.png){width="700" zoomable="yes"}

1. 将&#x200B;**自定义域URL**&#x200B;添加到&#x200B;**[!UICONTROL Asset Custom Domain]**&#x200B;字段。

1. 单击&#x200B;**[!UICONTROL Save Config]**&#x200B;以应用更新并启动资产同步。

## 下一步

* **配置您的Commerce店面** — 要将AEM Assets与由Edge Delivery Services提供支持的Commerce店面一起使用，请完成[Adobe Commerce店面文档](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/?lang=zh-Hans)的&#x200B;*AEM Assets集成*&#x200B;主题中所述的店面配置。

* 在Adobe Commerce与AEM Assets集成之间设置[匹配规则](../synchronize/default-match.md)。

* [管理Commerce资源](../manage-assets.md)。
