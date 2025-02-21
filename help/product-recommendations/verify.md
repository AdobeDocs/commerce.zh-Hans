---
title: 验证事件集合
description: 了解如何验证行为数据是否已发送到Adobe Commerce。
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# 验证事件集合

在[安装和配置](install-configure.md) `magento/product-recommendations`模块后，您可以验证行为数据是否已发送到Adobe Commerce。 您可以使用Chrome中提供的开发人员工具，或安装Snowplow Chrome扩展。 如果需要其他帮助，请参阅支持知识库中的[疑难解答 [!DNL Product Recommendations] 模块](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/troubleshoot-product-recommendations-module-in-magento-commerce.html)。

## 使用Chrome中的开发人员工具进行验证

要确保在所有网站页面上加载事件收集器JS文件，请执行以下操作：

1. 在Chrome中，选择&#x200B;**自定义和控制Google Chrome**，然后选择&#x200B;**更多工具** > **开发人员工具**。
1. 选择&#x200B;**网络**&#x200B;选项卡，然后选择&#x200B;**JS**&#x200B;类型。
1. `ds.`的筛选器
1. 重新加载页面。
1. 您应会在&#x200B;**Name**&#x200B;列中看到`ds.js`或`ds.min.js`。

![事件收集器JS](assets/filter-ds.png)
_事件收集器JS_

要确保整个网站（主页、产品、结帐等）的页面上触发事件，请执行以下操作：

1. 请确保在浏览器上禁用所有广告拦截器，并在网站上接受Cookie。
1. 在Chrome中，选择&#x200B;**自定义和控制Google Chrome**（浏览器右上角的三个垂直点），然后选择&#x200B;**更多工具** > **开发人员工具**。
1. 选择&#x200B;**网络**&#x200B;选项卡并筛选`tp2`。
1. 重新加载页面。
1. 您应会在&#x200B;**Name**&#x200B;列中看到`tp2`下的调用。

![正在触发事件](assets/filter-tp2.png)
_验证事件是否正在触发_

## 使用Snowplow Chrome扩展进行验证

安装适用于Chrome](https://chrome.google.com/webstore/detail/snowplow-analytics-debugg/jbnlcgeengmijcghameodeaenefieedm)的[Snowplow Analytics Debugger扩展。 此扩展显示正在收集并发送到Adobe Commerce的事件。

1. 请确保在浏览器上禁用所有广告拦截器，并在网站上接受Cookie。

1. 在Chrome中，选择&#x200B;**自定义和控制Google Chrome**（浏览器右上角的三个垂直点），然后选择&#x200B;**更多工具** > **开发人员工具**。

1. 选择&#x200B;**Snowplow Analytics调试器**&#x200B;选项卡。

1. 在&#x200B;**事件**&#x200B;列下，选择&#x200B;**结构化事件**。

1. 向下滚动直到看到&#x200B;**上下文数据&#x200B;_n_**为止。 在&#x200B;**架构**中查找店面实例。

1. 验证是否已正确设置[SaaS数据空间ID](https://experienceleague.adobe.com/docs/commerce-admin/config/services/saas.html)。

![雪铲过滤器](assets/snowplow-filter.png)
_雪铲过滤器_

>[!NOTE]
>
> 调试器中的值`Data validity : NOT FOUND`表示内部架构。 Snowplow Chrome插件无法验证具有内部架构的事件。 这不会对实际功能产生影响。

## 验证事件是否正确触发

要验证用于量度的事件是否正确触发，请在Snowplow Analytics调试器中查找`impression-render`、`view`和`rec-click`事件。 查看[事件的完整列表](https://experienceleague.adobe.com/docs/commerce/product-recommendations/developer/events.html)。

>[!NOTE]
>
> 如果启用了[Cookie限制模式](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html)，则在购物者同意之前，Adobe Commerce不会收集行为数据。 如果“Cookie限制模式”被禁用，则默认情况下会收集行为数据。
