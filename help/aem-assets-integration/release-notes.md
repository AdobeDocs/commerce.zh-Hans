---
title: AEM Assets集成发行说明
description: 有关所有AEM Assets集成版本的信息，请参阅发行说明。
feature: CMS, Media, Release Notes
exl-id: 0d639565-812f-481a-afd6-6e6fa54ed70e
source-git-commit: 89091ee8a69259ad325a2b2d7ed8d522fe23fac9
workflow-type: tm+mt
source-wordcount: '617'
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

_2025年9月11日_

![新问题](../assets/new.svg)已更新具有新[属性的](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/synchronize/custom-match){target=_blank}自定义自动匹配`asset_matches`端点。

_2025年2月11日_

![新问题](../assets/new.svg)现在，商家可以同步产品和类别的图像。

+++

## v1.2.7

_2025年11月6日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.5及更高版本。

![修复了问题](../assets/fix.svg)<!-- Issue ACAP-1169 -->修复了在&#x200B;**迷你购物车**、**购物车**&#x200B;和&#x200B;**结帐**&#x200B;页面上启用AEM Assets集成后，产品缩略图图像显示不一致的问题。 现在，即使刷新页面后，产品图像也会在所有页面中一致呈现。

## v1.2.6

_2025年10月24日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.5及更高版本。

![修复了问题](../assets/fix.svg)<!-- Issue ACAP-1163 -->解决了连续批量产品更新请求可能会导致状态跟踪标志卡住，从而阻止正确处理后续更新的问题。 现在，即使发生错误，状态也会重置。

## v1.2.5

_2025年10月22日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.5及更高版本。

![修复了问题](../assets/fix.svg)<!-- Issue ACAP-1161 -->修复了在Adobe Commerce管理中更新现有图像映射位置会导致PHP类型错误的问题。

## v1.2.4

_2025年10月17日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.5及更高版本。

![修复了问题](../assets/fix.svg)<!-- Issue ACAP-1155 -->改进了自定义属性的整体稳定性。 使用异步API时，自定义属性现在可以正确更新。

![修复了问题](../assets/fix.svg)<!-- Issue ACAP-1074 -->现在，定义基本链接URL时，[product-asset同步](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/store-urls#configure-the-base-url){target=_blank}不会失败。

## v1.2.3

_2025年10月2日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.5及更高版本。

![修复了问题](../assets/fix.svg)<!-- Issue ACAP-1135 -->修复了更新产品属性时出现的问题。 现在，产品属性会按预期更新，并在更新失败时返回相应的错误而不是200响应。

## v1.2.2

_2025年9月18日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.5及更高版本。

![已修复问题](../assets/fix.svg)<!-- Issue ACAP-1110 -->已改进迷你购物车、购物车和结帐页面上的整体图像稳定性。 这些页面上的图像现在可以正确加载。

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
