---
title: 处理Cookie限制
description: 了解产品推荐如何处理Cookie限制。
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# 处理Cookie限制

Adobe Commerce和Magento Open Source都会在数据存储在浏览器Cookie中之前请求同意。 有关详细信息，请参阅[Cookie限制模式](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html)。

将`magento/product-recommendations`模块部署到生产环境时，它会开始收集店面上的购物者交互事件。 由于这些事件的数据可以存储在浏览器Cookie或本地存储中，因此该功能支持Cookie限制模式，因为它在购物者同意Cookie之前不收集事件。

这可能不适用于第三方Cookie同意解决方案。 每个商家都有责任确保在获得Cookie同意之前不会收集数据，法律通常要求这样做。 如果您通过自定义代码管理Cookie同意，则可以使用名为`mg_dnt`的不跟踪Cookie来限制数据收集。

- Cookie的名称：

  ```text
  `const DNT_COOKIE = "mg_dnt";`
  ```

- 设置do-not-track Cookie以禁用数据收集：

  ```text
  `$.mage.cookies.set(DNT_COOKIE, true);`
  ```

- 要在用户接受Cookie时清除Cookie，请执行以下操作：

  ```text
  `$.mage.cookies.clear(DNT_COOKIE);`
  ```
