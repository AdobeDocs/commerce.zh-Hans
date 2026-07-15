---
title: 配置您的店面
description: 了解如何将Edge Delivery Services店面连接到AEM Assets集成。
feature: CMS, Media, Integration
TQID: https://experienceleague.adobe.com/gl0Y2UNs3sYkXE9QYwLtAltyX1dxE699y23ey-y0KUU
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
subfeature_v2: id: ae62cf09-5996-4921-bda8-fbe67b62e470
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2: id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: 7f901cec90291e264376e3f93e6ebaaccf7c15f0
workflow-type: tm+mt
source-wordcount: 610
ht-degree: 0%

---

# 配置您的店面

## 从AEM Assets启用产品图像显示 {#enable-product-images}

AEM Assets集成显示AEM Assets而不是Adobe Commerce中的产品图像，从而实现高级优化、裁剪和CDN交付。

要在Edge Delivery Services支持的Commerce店面中启用集成，请将`"commerce-assets-enabled": true`参数添加到店面配置文件(`config.json`)。

```json
{
  "public": {
    "default": {
      "commerce-assets-enabled": true
    }
  }
}
```

Commerce下拉列表会自动检测`commerce-assets-enabled`配置并相应地调整图像处理。

有关将AEM Assets与由Edge Delivery Services提供支持的Commerce店面结合使用的更多信息，请参阅&#x200B;*AEM Assets店面*&#x200B;文档中的[Adobe Commerce集成](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/)主题。

>[!TIP]
>
>要允许作者浏览并将AEM Assets插入静态内容页面，请参阅[将AEM Assets连接到Da.live以进行静态内容创作](#connect-aem-assets-authoring)。

## 将AEM Assets连接到Da.live以进行静态内容创作 {#connect-aem-assets-authoring}

>[!NOTE]
>
>此设置独立于AEM Assets集成扩展。 它由[Da.live](https://da.live){target="_blank"}提供，允许作者通过[!UICONTROL Library]面板和[!UICONTROL Content Advisor]浏览并将AEM Assets插入静态内容页面（例如，登陆页面或内容块）。 通过AEM Assets集成同步的产品图像是使用`commerce-assets-enabled`设置单独配置的。

使用以下步骤将AEM Assets连接到文档创作(Da.live)店面，以便在编辑静态内容时，作者可以浏览并插入&#x200B;**[!UICONTROL Content Advisor]**&#x200B;中的AEM Assets。

>[!NOTE]
>
>有关详细的设置说明，请参阅Da.live文档中的[设置AEM Assets](https://docs.da.live/administrators/guides/setup-aem-assets){target=_blank}和AEM Assets文档中的[在为AEM Assets创作内容时集成Edge Delivery Services](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/integrate-aem-assets-edge-delivery-services/integrate-aem-assets-edge-delivery-services){target=_blank}。

### 步骤1：在Da.live中打开您的站点配置

1. 从[Da.live](https://da.live){target=_blank}，找到并打开您的店面。

1. 在痕迹导航中，选择网站名称旁边的&#x200B;**[!UICONTROL Settings]**&#x200B;图标以打开网站配置电子表格。

### 步骤2：复制AEM存储库URL

1. 在新选项卡中，转到[experience.adobe.com](https://experience.adobe.com){target=_blank}并导航到&#x200B;**[!UICONTROL Experience Manager]**。

1. 打开Adobe Experience Manager Assets：滚动到&#x200B;**[!UICONTROL My Authoring]**&#x200B;部分，然后选择&#x200B;**[!UICONTROL Production]**&#x200B;环境旁边的&#x200B;**[!UICONTROL Assets]**。

1. 从浏览器地址栏中，复制以`author`开头的区段到`.com`并且包括，例如`author-p107634-e1009805.adobeaemcloud.com`。

### 步骤3：将存储库ID添加到您的配置

1. 要配置您的站点，请返回到Da.live并在站点配置中选择&#x200B;**[!UICONTROL data]**。

1. 按如下方式填写电子表格：

   | 单元格 | 值 |
   |---|---|
   | A1 | `key` |
   | B1 | `value` |
   | A2 | `aem.repositoryId` |
   | B2 | 您在步骤2中复制的URL |

1. 选择&#x200B;**[!UICONTROL Save]**，然后选择站点名称旁边的“上一步”箭头以返回到站点根目录。

   >[!NOTE]
   >
   > 带有前缀的`author-`主机从创作层浏览资产。 要改为通过Dynamic Media投放资源，请使用前缀为`delivery-`的主机。 有关所有`aem.repositoryId`选项，请参阅[设置AEM Assets](https://docs.da.live/administrators/guides/setup-aem-assets){target=_blank}。

### 步骤4：通过库连接AEM Assets

1. 从站点根目录中，选择&#x200B;**[!UICONTROL index]**&#x200B;文件夹以将其打开。

1. 在编辑器中，打开&#x200B;**[!UICONTROL Library]**&#x200B;面板并选择&#x200B;**[!UICONTROL AEM Assets]**。

   **[!UICONTROL Content Advisor]**&#x200B;弹出窗口将打开并显示您的AEM Assets文件夹和文件。

您的店面现已连接到AEM Assets。 您可以直接从&#x200B;**[!UICONTROL Content Advisor]**&#x200B;浏览和插入资源。

## 相关文档

* *AEM Assets Storefront*&#x200B;文档中的[Adobe Commerce集成](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/){target=_blank} — 店面配置和图像处理行为。

* 在&#x200B;*AEM Assets*&#x200B;文档中为Edge Delivery Services](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/integrate-aem-assets-edge-delivery-services/integrate-aem-assets-edge-delivery-services){target=_blank}创作内容时，[集成AEM Assets。

* 在Da.live文档中[设置AEM Assets](https://docs.da.live/administrators/guides/setup-aem-assets){target=_blank}和[使用媒体](https://docs.da.live/authors/guides/adding-media){target=_blank}。
