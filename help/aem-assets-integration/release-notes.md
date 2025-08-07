---
title: AEM Assets集成发行说明
description: 有关所有AEM Assets集成版本的信息，请参阅发行说明。
feature: CMS, Media, Release Notes
exl-id: 0d639565-812f-481a-afd6-6e6fa54ed70e
source-git-commit: ff6affa5bcc4111e14054f3f6b3ce970619ca295
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# AEM Assets集成发行说明

以下发行说明介绍了AEM Assets集成的初始版本，其中包括：

![新](../assets/new.svg)新功能
![已修复问题](../assets/fix.svg)修复和改进
![已知问题](../assets/bug.svg)已知问题

有关在常规功能发布版本之外发布的功能更改和修复，请查看&#x200B;_托管服务更新_&#x200B;部分。

有关即将发行的版本、产品支持以及哪些Adobe Commerce版本支持AEM Assets集成扩展的详细信息，请参阅Adobe Commerce [发行计划](https://experienceleague.adobe.com/en/docs/commerce-operations/release/planning/schedule)和[产品可用性](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability)主题。

## 托管服务更新

这些发行说明描述了所发生以及发行的功能更改和修复，这些更改和修复超出了托管服务的常规功能发行版本。

+++托管服务更新

_2025年2月11日_

![新问题](../assets/new.svg)现在，商家可以同步产品和类别的图像。

+++

## v1.2.0

_2025年8月7日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.5及更高版本。

![新问题](../assets/new.svg)<!-- Issue ACAP-1018 -->现在，商家可以通过在管理员中配置Assets集成时选择[可视化所有者](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/setup-synchronization){target=_blank}来选择图像和媒体资源的源。

![新问题](../assets/new.svg)<!-- Issue ACAP-1078 -->已更新具有新[属性的](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/synchronize/custom-match){target=_blank}自定义自动匹配`asset_matches`端点。 此更改允许您实施自己的匹配逻辑以返回与特定`productSku`关联的所有资产。

## v1.1.2

_2025年6月11日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.5及更高版本。

![新问题](../assets/new.svg)<!-- Issue ACAP-1041 -->添加了对Adobe Commerce 2.4.8和PHP 8.4的支持。

## v1.1.0

_2025年4月23日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.5及更高版本。

![新问题](../assets/new.svg)<!-- Issue ACAP-955 -->现在，可以使用[自定义域URL](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/setup-synchronization#optional-configure-the-custom-domain-url)而不是AEM投放URL。 如果商家在其AEM功能板中设置了&#x200B;**自定义域名**，则需要在Commerce中添加此&#x200B;**自定义域URL**。

![修复了问题](../assets/fix.svg)<!-- Issue ACAP-987 -->改进了AEM Assets同步过程的整体日志。

## v1.0.22

_2025年3月12日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.5及更高版本。

![新问题](../assets/new.svg)<!-- Issue ACAP-xx -->现在，Assets选择器需要[Assets选择器IMS客户端ID](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/setup-synchronization)，才能将AEM Assets图像映射到产品类别和页面生成器生成的内容。

## v1.0.20

_2025年2月11日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.5及更高版本。

![新](../assets/new.svg)<!-- Issue ACAP-xx -->一般可用性版本。
