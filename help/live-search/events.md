---
title: '[!DNL Live Search]个事件'
description: 了解事件如何收集 [!DNL Live Search]的数据。
feature: Services, Eventing
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---

# [!DNL Live Search]个事件

[!DNL Live Search]使用事件来增强搜索算法，例如“查看次数最多”和“查看了这个项目，查看了那个项目”。 虽然[Commerce示例Luma主题](https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/design/themes/themes#the-default-theme)开箱即用地事件，但Headless和其他自定义实施必须根据自己的需求实施事件。

此表描述了[!DNL Live Search] [排名策略](rules-add.md#intelligent-ranking)使用的事件。

| 排名策略 | 活动 | 页面 |
| --- | --- | --- |
| 查看次数最多 | `page-view`<br>`product-view` | 产品详细信息页面 |
| 购买次数最多 | `page-view`<br>`complete-checkout` | 购物车/结帐 |
| 添加到购物车的次数最多 | `page-view`<br>`add-to-cart` | 产品详细信息页面<br>产品列表页面<br>购物车<br>愿望清单 |
| 查看了这个项目，也查看了那个项目 | `page-view`<br>`product-view` | 产品详细信息页面 |

>[!NOTE]
>
>为[!DNL Live Search]目的的数据收集不包括个人身份信息(PII)。 所有用户标识符（如Cookie ID和IP地址）都经过严格匿名处理。 [了解更多](https://www.adobe.com/privacy/experience-cloud.html)。

## 必需的报告面板事件

需要一些事件来填充[实时搜索仪表板](performance.md)

| 仪表板区域 | 活动 | 加入字段 |
| ------------------- | ------------- | ---------- |
| 独特搜索 | `page-view`，`search-request-sent`，`search-response-received` | `searchRequestId` |
| 零结果搜索 | `page-view`，`search-request-sent`，`search-response-received` | `searchRequestId` |
| 零结果率 | `page-view`，`search-request-sent`，`search-response-received` | `searchRequestId` |
| 热门搜索 | `page-view`，`search-request-sent`，`search-response-received` | `searchRequestId` |
| 平均 点击位置 | `page-view`，`search-request-sent`，`search-response-received`，`search-results-view`，`search-product-click` | `searchRequestId` |
| 点进率 | `page-view`，`search-request-sent`，`search-response-received`，`search-results-view`，`search-product-click` | `searchRequestId`，`sku`，`parentSku` |
| 转化率 | `page-view`，`search-request-sent`，`search-response-received`，`search-results-view`，`search-product-click`，`product-view`，`add-to-cart`，`place-order` | `searchRequestId`，`sku`，`parentSku` |

### 所需上下文

所有事件都需要`Page`和`Storefront`上下文。 这应在页面级别/店面应用程序层发生，而不是在生成单个事件时发生（例如，在PHP店面中，PHP应用程序容器负责在运行时设置它们）。

## 使用情况

以下是`search-request-sent`事件的实现示例：

```javascript
const mse = window.magentoStorefrontEvents;

/* set in application container */
// mse.context.page(pageCtx);
// mse.context.setStorefrontInstance(storefrontCtx);

/* set before firing event */
mse.context.setSearchInput(searchInputCtx);
mse.publish.searchRequestSent("search-bar");
```

## 注意事项

- 广告拦截器和隐私设置可能会阻止捕获事件，并可能导致参与和收入[量度](performance.md)少报。 此外，由于购物者离开页面或网络问题，某些事件可能无法发送。
- Headless实施必须实施事件以推动智能促销。

>[!NOTE]
>
>如果启用了[Cookie限制模式](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html)，则在购物者同意使用Cookie之前，Adobe Commerce不会收集行为数据。 如果“Cookie限制模式”被禁用，Adobe Commerce会默认收集行为数据。
