---
title: 配置您的店面
description: 了解如何将Edge Delivery Services店面连接到AEM Assets集成。
feature: CMS, Media, Integration
source-git-commit: d426c7878f7a66fe1047673be7c5bf65ae1949a7
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---


# 配置您的店面

AEM Assets集成显示在AEM Assets中管理的产品图像，而不是使用在Adobe Commerce中托管的图像。 该集成支持增强的映像管理功能，包括通过Adobe的内容交付网络(CDN)进行的高级优化、裁剪和交付。

要在Edge Delivery Services支持的Commerce店面中启用集成，请更新店面配置文件(`config.json`)以添加`"commerce-assets-enabled": true`参数。

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

有关如何将AEM Assets与由Edge Delivery Services提供支持的Commerce店面结合使用的更多信息，请完成[AEM Assets店面](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/)文档中的&#x200B;*Adobe Commerce集成*&#x200B;主题中所述的店面配置。
