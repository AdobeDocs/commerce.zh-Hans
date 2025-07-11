---
title: 配置集成
description: 了解如何将Adobe Commerce项目与Experience Manager Assets项目连接起来，以便在这两个系统之间启用资源同步。
feature: CMS, Media
exl-id: 3533d010-926f-4d78-935c-98a9b7040d27
source-git-commit: 995fb071953ddad6cb2076207910679905bb0347
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 0%

---

# 配置集成

通过将Commerce连接到AEM Assets实例并选择资源同步的匹配策略来配置集成。

识别AEM Assets项目后，选择用于在Adobe Commerce和AEM Assets之间同步资产的匹配规则。

* **[!UICONTROL Match by product SKU]** — 将资源元数据中的SKU与[Commerce产品SKU](https://experienceleague.adobe.com/zh-hans/docs/commerce-operations/implementation-playbook/glossary#sku)匹配的默认规则，以确保资源与正确的产品关联。

* **[!UICONTROL Custom match]** — 匹配规则，用于需要自定义匹配逻辑的更复杂方案或特定业务要求。 实施自定义匹配需要在Adobe Developer App Builder中开发自定义代码以定义资源与产品的匹配方式。 更多详细信息即将推出……

对于初始设置，使用默认的&#x200B;*按产品SKU匹配*&#x200B;规则。

## 先决条件

* [安装AEM Assets包](configure-aem.md)

* [!BADGE 仅限PaaS]{type=Informative tooltip="仅适用于云项目上的Adobe Commerce(Adobe管理的PaaS基础架构)。"} [安装Adobe Commerce包](configure-commerce.md)以添加扩展并生成使用该扩展所需的凭据和连接。

* 按照[启用Dynamic Media Open API](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/dynamic-media-open-apis-overview#enable-dynamic-media-open-apis)主题中描述的步骤操作。 请向支持团队提供以下信息：

   * **[!UICONTROL AEM Program ID]**
   * **[!UICONTROL Adobe Commerce URL]**
   * **[!UICONTROL AEM Environment ID]**，
   * 要连接到Commerce的AEM Assets创作环境的&#x200B;**[!UICONTROL IMS Org ID]**。

## 配置连接

1. 获取[AEM Assets创作环境](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/sites/authoring/quick-start)项目和环境ID。

   1. 打开AEM Cloud Manager并选择&#x200B;**[!UICONTROL Assets]**。

   1. 从URL <br>`https://author-p[Program ID]-e[EnvironmentID].adobeaemcloud.com/`复制并保存项目和环境ID

1. 从Commerce管理员中，打开AEM Assets集成配置。

   1. 转到&#x200B;**[!UICONTROL Store]** >配置> **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**。

      ![AEM Assets集成启用该集成](../assets/aem-assets-integration-enable-config.png){width="600" zoomable="yes"}

1. 进入AEM Assets环境&#x200B;**[!UICONTROL Program ID]**&#x200B;和&#x200B;**[!UICONTROL Environment ID]**。

   通过从&#x200B;*[!UICONTROL Use system value]*&#x200B;中删除所选内容来编辑配置值。

1. 输入&#x200B;**[!UICONTROL Asset Selector IMS Client ID]**。

   有关资产选择器的详细信息，请参阅[手动选择资产](../synchronize/asset-selector-integration.md)

1. [!BADGE 仅限PaaS]{type=Informative tooltip="仅适用于云项目上的Adobe Commerce(Adobe管理的PaaS基础架构)。"}选择[[!UICONTROL Commerce integration]](configure-commerce.md#add-the-integration-to-the-commerce-environment)以在Commerce和资源匹配服务之间验证请求。

1. 将&#x200B;**[!UICONTROL Integration enabled]**&#x200B;设置为`Yes`以允许Commerce接受来自AEM Assets的传入更新。

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

### 可选。 配置自定义域URL

如果已为AEM Assets as a Cloud Service项目配置了[自定义域名](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name){target=_blank}，则必须将该域名添加到Commerce存储配置，以便Commerce的AEM Assets集成可以使用该域名。

1. 导航到&#x200B;**[!UICONTROL Store]** >配置> **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**。

   ![AEM Assets集成启用该集成](../assets/aem-assets-view.png){width="600" zoomable="yes"}

1. 将&#x200B;**自定义域URL**&#x200B;添加到&#x200B;**[!UICONTROL Asset Custom Domain]**&#x200B;字段。

1. 单击&#x200B;**[!UICONTROL Save Config]**&#x200B;以应用更新并启动资产同步。

## 下一步

[管理Commerce资源](../manage-assets.md)
