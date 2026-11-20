---
title: 配置集成
description: 了解如何将Adobe Commerce项目与Experience Manager Assets项目连接起来，以便在这两个系统之间启用资源同步。
feature: CMS, Media
exl-id: 3533d010-926f-4d78-935c-98a9b7040d27
TQID: 'https://experienceleague.adobe.com/MM-neGrH-N8xBcCwLgnsaIrIjhbX6uYL5kS41QdV79I'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: ddbd0f6e-b569-5a04-8a70-55058777c373
    internal-label: CMS
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
    internal-label: Storefront configuration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: 5e9c42e5c93ac81604aa38bf3e55c5df729650a0
workflow-type: tm+mt
source-wordcount: '1355'
ht-degree: 1%
---
# 配置集成

通过将Commerce连接到AEM Assets实例并选择资源同步的匹配策略来配置集成。

识别AEM Assets项目后，选择用于在Adobe Commerce和AEM Assets之间同步资产的匹配规则。

* **[!UICONTROL Match by product SKU]** — 将资源元数据中的SKU与[Commerce产品SKU](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/glossary#sku)匹配的默认规则，以确保资源与正确的产品关联。

* **[!UICONTROL Custom match]** — 匹配规则，用于需要自定义匹配逻辑的更复杂方案或特定业务要求。 实施自定义匹配需要在Adobe Developer App Builder中开发自定义代码以定义资源与产品的匹配方式。 请参阅[自定义自动匹配](../synchronize/custom-match.md)。

对于初始设置，请使用默认&#x200B;**[!UICONTROL Match by product SKU]**&#x200B;规则。

## 要求

在配置AEM Assets集成之前，请验证您已完成以下步骤：

* [配置AEM Assets项目](configure-aem.md)

* [!BADGE 仅限PaaS]{type=Informative tooltip="仅适用于云项目上的Adobe Commerce（Adobe管理的PaaS基础架构）。"} [安装Adobe Commerce包](configure-commerce.md)以添加扩展并生成使用该扩展所需的凭据和连接。

* [用户权限和IMS](permissions.md) — 配置资产选择器、AEM环境选择和域映射所需的权限。

## 配置连接

![AEM Assets集成配置具有示例环境和域值](../assets/aem-assets-view.png){width="900" zoomable="yes"}

1. 从Commerce管理员转到&#x200B;**[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**。

>[!INFO]
>
> AEM Assets集成仅支持全局（默认）范围内的配置。 不支持网站级别的配置。 当您尝试在网站级别配置集成时，系统会忽略网站级别的设置，而使用全局配置值。

1. 仅[!BADGE PaaS]{type=Informative tooltip="仅适用于云项目上的Adobe Commerce（Adobe管理的PaaS基础架构）。"}输入&#x200B;**[!UICONTROL Asset Selector IMS Client ID]**。

   启用资产选择器需要此ID。 请参阅[用户权限和IMS](permissions.md)以获取此ID。 有关资产选择器的详细信息，请参阅[手动选择资产](../synchronize/asset-selector-integration.md)。

1. 从&#x200B;**[!UICONTROL AEM Environment]**&#x200B;中，选择在[配置AEM Assets项目](configure-aem.md)中配置的环境。

   该列表包括您的用户具有“创作”或“交付”产品配置文件的AEM环境。 如果缺少所需的环境，请检查[用户权限和IMS](permissions.md)。

   如果您的配置显示单独的&#x200B;**[!UICONTROL Program ID]**&#x200B;和&#x200B;**[!UICONTROL Environment ID]**&#x200B;字段，请指定该环境的标识符。 对于手动输入，请从AEM Cloud Manager复制它们，或从创作URL派生它们： `https://author-p<ProgramID>-e<EnvironmentID>.adobeaemcloud.com/`。 仅输入数字标识符，不带`p`和`e`前缀。

   对于具有&#x200B;**[!UICONTROL Use system value]**&#x200B;复选框的字段，请在覆盖默认值之前清除该复选框。

1. 检查&#x200B;**[!UICONTROL AEM Domain Mapping]**。 可用域会根据选定的AEM环境自动加载。 如果您的项目使用自定义资产交付域，请按照[配置自定义域URL](#optional-configure-the-custom-domain-url)操作。

1. [!BADGE 仅限PaaS]{type=Informative tooltip="仅适用于云项目上的Adobe Commerce（Adobe管理的PaaS基础架构）。"}选择[[!UICONTROL Commerce integration]](configure-commerce.md#add-the-integration-to-the-commerce-environment)以在Commerce和资源匹配服务之间验证请求。

1. 将&#x200B;**[!UICONTROL Synchronization enabled]**&#x200B;设置为`Yes`以允许Commerce接受来自AEM Assets的传入更新。

   启用集成后，可以使用其他配置选项来指定资源匹配条件。

1. 从&#x200B;**[!UICONTROL Asset matching rule]**&#x200B;下拉列表中选择一个资源匹配规则以进行资源同步。

   * [的Select **[!UICONTROL Match by product SKU]**&#x200B;默认自动匹配](../synchronize/default-match.md)。
   * 用于[自定义自动匹配](../synchronize/custom-match.md)的Select **[!UICONTROL Custom match]**。 此选项需要[Adobe Developer App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/extensibility/adobe-developer-app-builder/introduction-to-app-builder)。

1. 对于&#x200B;**[!UICONTROL Match by product SKU]**，在&#x200B;**[!UICONTROL Match by product SKU attribute name]**&#x200B;字段中输入[AEM Assets元数据属性名称](../metadata.md)。 默认值为`commerce:skus`。

   输入属性名称，而不是产品SKU值。 将实际产品SKU添加到AEM Assets中每个资源的&#x200B;**[!UICONTROL Product Data]**&#x200B;元数据，如[默认自动匹配](../synchronize/default-match.md)中所述。

1. 查看[可视化图表所有者](#configure-the-visualization-owner)设置。 在迁移过程中，保留&#x200B;**Adobe Commerce**&#x200B;所有权，直到资产同步完成。

1. 选择&#x200B;**[!UICONTROL Save Config]**&#x200B;以应用更新并启动资产同步。

   配置更新会触发初始同步过程，从而允许Commerce接受来自AEM Assets的传入更新。 同步所需的时间取决于资产量和特定配置。 该集成利用自动化流程来最大限度地减少同步所需的时间。

### 同步SLA

集成的service level agreement (SLA)保证了以下同步性能级别：

* `< 5 minutes for 99% of updates`

* `< 30 minutes for 99.9% of updates`

这一级别的服务可确保产品页面始终显示最新的图像，使店面内容准确且具有视觉吸引力。

## 同步本地化的替换文本

本地化的替换文本使用现有的资源同步过程。 您不需要新的事件类型或单独的同步配置。

1. 在AEM资源的&#x200B;**[!UICONTROL Commerce]**&#x200B;选项卡中添加一个或多个存储视图替换文本行。

1. 将资产与Commerce产品SKU关联。

1. 在AEM Assets中批准资源。

1. 等待资产事件和同步过程完成。

1. 验证Commerce管理员和店面响应中的本地化值。

有关字段名称、验证规则和Commerce结果，请参阅AEM Assets中的[Commerce元数据](../metadata.md)。

## 配置可视化图表所有者

**可视化所有者**&#x200B;设置确定在集成中提供产品图像的系统：

* Adobe Commerce — 使用在Commerce中托管的图像。

* AEM Assets — 使用从AEM同步的图像。

管理员显示该所有者的可用图像，而其余图像则呈灰显状态，并带有&#x200B;**hidden**&#x200B;标签。

有关图像显示行为的详细信息，请参阅[设置图像详细信息](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/digital-assets/product-image#set-image-details){target=_blank}主题。

>[!TIP]
>
> 从Commerce迁移到AEM Assets期间，请将&#x200B;**可视化所有者**&#x200B;设置为Commerce以避免图像链接损坏。 成功与AEM Assets同步所有产品后，切换到AEM Assets所有者以完成过渡。 这可以确保映像在整个过程中持续可用。

1. 导航到&#x200B;**[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**。

   将![可视化所有者设置为AEM Assets](../assets/visualization-owner-detail.png){width="700" zoomable="yes"}

1. Select **可视化所有者**&#x200B;源以显示图像。

1. 单击&#x200B;**[!UICONTROL Save Config]**&#x200B;以应用更新。

   在切换到&#x200B;**AEM Assets**&#x200B;之前，[请验证资源是否与预期的产品](#verify-the-integration)相关联。 然后[配置您的店面](configure-storefront.md)以显示AEM Assets产品图像。

## 可选。 配置自定义域URL

如果已为AEM Assets as a Cloud Service项目配置了[自定义域名](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name){target=_blank}，则必须将该域名添加到Commerce存储配置，以便Commerce的AEM Assets集成可以使用该域名。

从AEM管理员处获取配置的资源投放自定义域URL。 此设置取代了AEM投放URL；它不是用于标识项目ID和环境ID的AEM创作URL。 如果您的项目不使用自定义域，则保持域映射不变。

>[!NOTE]
>
>配置自定义域URL不会更新以前同步的资源的URL。 这些资源保留其以前的URL，直到在AEM Assets](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/reprocessing){target=_blank}中重新处理[为止。 保存自定义域配置后，重新处理这些资产以更新其URL以使用自定义域。

1. 导航到&#x200B;**[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**。

1. 确认选定的&#x200B;**[!UICONTROL AEM Environment]**，然后从&#x200B;**[!UICONTROL AEM Domain Mapping]**&#x200B;中选择配置的自定义域。 将为所选环境自动加载可用域。

![具有示例值的AEM环境和域选择器](../assets/aem-assets-environment-domain.png){width="700" zoomable="yes"}

    对于显示**[!UICONTROL Asset Custom Domain]**文本字段的配置，请在该字段中输入自定义域URL。

1. 单击&#x200B;**[!UICONTROL Save Config]**&#x200B;以应用更新。

## 验证集成

>[!NOTE]
>
>同步状态不适用于Adobe Commerce Optimizer。 请按照[Commerce Optimizer验证工作流](configure-aco.md#match-by-sku-workflow-example)进行操作，而不是执行下面的Commerce管理员检查。

1. 选择现有的Commerce产品并记下其SKU。

1. 在AEM Assets中，将测试资产标记为&#x200B;**[!UICONTROL Eligible for Commerce]**，将其与该产品SKU相关联，并设置其角色和位置。 批准资产。 查看[默认自动匹配](../synchronize/default-match.md)，或使用您配置的[自定义匹配规则](../synchronize/custom-match.md)。

1. 同步完成后，在Commerce管理员中打开该产品，并检查其&#x200B;**[!UICONTROL Images And Videos]**&#x200B;部分中的相关资源、角色和位置。 请参阅[管理资源](../manage-assets.md)。

1. 查看[同步状态](sync-status.md)以了解资产的同步结果。 如果同步失败，请查看&#x200B;**[!UICONTROL Error]**&#x200B;列。

1. 选择&#x200B;**AEM Assets**&#x200B;作为可视化图表所有者并完成[店面配置](configure-storefront.md)后，在店面中打开产品并确认显示预期的图像。

仅[!BADGE PaaS]{type=Informative tooltip="仅适用于云项目上的Adobe Commerce（Adobe管理的PaaS基础架构）。"}有关其他同步疑难解答，请查看[集成日志](logs.md)。

## 下一步

* [配置您的Commerce店面](configure-storefront.md)，以便使用Edge Delivery Services显示AEM Assets中的产品图像。

* 在Adobe Commerce与AEM Assets集成之间设置[匹配规则](../synchronize/default-match.md)。

* [管理Commerce资源](../manage-assets.md)。
