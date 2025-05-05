---
title: '[!DNL Store Fulfillment by Walmart Commerce Technologies]发行说明'
description: 查看发行说明，了解所有 [!DNL Store Fulfillment by Walmart Commerce Technologies] 发行版本的信息。
role: Admin, User, Leader
feature: Shipping/Delivery, Release Notes
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---

# 发行说明

这些发行说明描述了[!DNL Store Fulfillment Services by Walmart Commerce Technologies]的初始版本，其中包括：

![新](../assets/new.svg)新功能
![已修复问题](../assets/fix.svg)修复和改进
![已知问题](../assets/bug.svg)已知问题

请参阅[即将发布的版本](https://experienceleague.adobe.com/docs/commerce-operations/release/planning/schedule.html?lang=zh-Hans)，了解版本计划和支持。

请参阅[产品可用性](https://experienceleague.adobe.com/docs/commerce-operations/release/product-availability.html?lang=zh-Hans)，了解哪些Adobe Commerce版本支持此扩展。

## v1.5.0

*2023年8月3日*

[!BADGE 支持]{type=Informative tooltip="支持"}[Adobe Commerce 2.4.4到2.4.6](https://experienceleague.adobe.com/docs/commerce-operations/release/product-availability.html?lang=zh-Hans)，包括2.4.6-p1、2.4.5-p3和2.4.4-p4安全修补程序版本

此版本包含以下更新：

![新](../assets/fix.svg)更新了扩展以支持[Adobe Commerce安全修补程序版本](https://experienceleague.adobe.com/docs/commerce-operations/release/notes/security-patches/overview.html?lang=zh-Hans) 2.4.6-p1、2.4.5-p3和2.4.4-p4。

![新](../assets/new.svg)<!-- WMTP-918 -->添加了对销售电子邮件的[异步发送](sales-emails.md)配置选项的支持。 升级到版本1.5.0的商家可以选择立即发送电子邮件（默认）或异步发送。

![新建](../assets/new.svg)<!-- WMTP-916-->已更新[源配置](merchant-store-configuration.md)以支持国际电话号码格式。

![新](../assets/new.svg)添加了用于防止退款金额超过剩余金额或开票金额的逻辑。

![New](../assets/new.svg)<!-- WMTP-882 -->已将`google.map.LatLng`对象替换为JSON文本，以支持与旧版[!DNL Google Maps]的兼容性。

![修复了问题](../assets/fix.svg)<!-- WMTP- -->更新了创建`[!DNL Available for Store Pickup]`和`[!DNL Available for Home Delivery]`产品属性的脚本以防止属性类别冲突。

![修复了问题](../assets/fix.svg)<!-- WMTP-915 -->修复了在加载和保存某些实体时导致无限循环的兼容性问题。

![修复了问题](../assets/fix.svg)<!-- WMTP-921 -->修复了在将项目从产品详细信息页面(PDP)添加到购物车时阻止触发[!DNL Ship to Store]报价验证的问题。

![修复了问题](../assets/fix.svg)<!-- WMTP- 932 -->修复了允许客户为不符合主页递送条件的项目选择主页递送方法的签出问题。

![已修复问题](../assets/fix.svg)安装更新：

- &#x200B;<!-- WMTP-880--> 修复了在安装[!DNL Store Fulfillment]扩展时导致返回错误网站代码的问题。

- &#x200B;<!-- WMTP-878--> 修复了SKU整数的一个问题，该问题要求在安装期间将数据类型转换为字符串类型。

![修复了问题](../assets/fix.svg)<!-- WMTP-915-->修复了因缺少签入错误代码导致的失败。

![修复了问题](../assets/fix.svg)<!-- WMTP-932 -->修复了与分配操作期间部分拒绝相关的错误。

![New](../assets/new.svg)<!-- WMTP-953 -->更新了Cancel API终结点，以将状态参数用作可选对象。

![新](../assets/new.svg)<!-- WMTP-960 -->改进了Dispense API端点的日志记录详细信息。

## v1.4.0

*2023年4月13日*

[!BADGE 支持]{type=Informative tooltip="支持"}

![新](../assets/fix.svg) [!DNL Store Fulfillment]现在[与 [!DNL Adobe Commerce] 2.4.4到2.4.6](https://experienceleague.adobe.com/docs/commerce-operations/release/product-availability.html?lang=zh-Hans)兼容。


## v1.3.0

*2023年2月27日*

[!BADGE 支持]{type=Informative tooltip="支持"}

此版本包含以下更新：

![新](../assets/fix.svg)<!-- WMTP-795 -->添加了一项功能，通过将系统配置设置的默认范围从网站更改为全局，禁用了特定站点的商店完成解决方案。

## v1.2.0

*2022年9月27日*

[!BADGE 支持]{type=Informative tooltip="支持"}

此版本包含以下更新：

![新](../assets/fix.svg) [!DNL Store Fulfillment]现在[与 [!DNL Adobe Commerce] 2.4.4到2.4.5](https://experienceleague.adobe.com/docs/commerce-operations/release/product-availability.html?lang=zh-Hans)兼容。


## v1.1.0

*2022年7月15日*

[!BADGE 支持]{type=Informative tooltip="支持"}

稳定性：正式发布

![新](../assets/fix.svg)<!-- WMTP-731 -->通过添加默认汽车制造和模型选择，简化了Store Assist应用程序的[登记体验配置](check-in-experience-setup.md)。 在以前的版本中，商家必须手动配置汽车厂牌和车型选择。

## v1.0.0

*2022年3月4日*

[!BADGE 支持]{type=Informative tooltip="支持"}

稳定性：正式发布

## 商店协助应用程序

有关Store Assist应用程序新版本的信息，请参阅[Apple App Store](https://apps.apple.com/us/app/store-assist-by-walmart/id1609281539){target="_blank"}或[Google Play应用商店](https://play.google.com/store/apps/details?id=com.walmart.faas.storeassist){target="_blank"}中的应用程序信息。
