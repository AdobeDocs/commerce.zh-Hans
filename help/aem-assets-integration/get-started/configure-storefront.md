---
title: 配置您的店面
description: 了解如何将Edge Delivery Services店面连接到AEM Assets集成。
feature: CMS, Media, Integration
TQID: https://experienceleague.adobe.com/gl0Y2UNs3sYkXE9QYwLtAltyX1dxE699y23ey-y0KUU
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 137
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

有关如何将AEM Assets与由Edge Delivery Services提供支持的Commerce店面结合使用的更多信息，请完成&#x200B;*AEM Assets店面*&#x200B;文档中的[Adobe Commerce集成](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/?lang=zh-Hans)主题中所述的店面配置。
