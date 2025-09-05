---
title: 处理Cookie限制
description: 了解产品推荐如何处理Cookie限制和隐私合规性。
exl-id: 7e7342db-b903-4105-93c0-e4022c81673b
source-git-commit: dbb36b9fa800e128f1aea795a891ffbfb751aa76
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 0%

---

# 处理Cookie限制

Adobe Commerce和Magento Open Source都会在数据存储在浏览器Cookie中之前请求同意。 有关详细信息，请参阅[Cookie限制模式](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html?lang=zh-Hans)。

## 产品推荐如何处理Cookie限制

将`magento/product-recommendations`模块部署到生产环境时，它将开始收集店面上的购物者交互事件。 此数据可以存储在浏览器Cookie或本地存储中，以支持推荐算法。

>[!IMPORTANT]
>
>现在，“产品推荐”遵循Cookie限制模式，在启用Cookie限制时，不会在Cookie或本地存储中收集或存储任何数据。 其中包括用于个性化推荐的行为数据。

### 受Cookie限制影响的数据

启用Cookie限制模式时，不会收集以下产品推荐数据：

- **行为数据**：产品查看、添加到购物车操作、购买和其他购物者交互。
- **会话数据**：购物者会话信息和推荐单元交互。
- **Personalization数据**：用于推荐类型（如“最近查看的”和“最购买的”）的数据。

### 对推荐类型的影响

启用Cookie限制模式且购物者未接受Cookie时，某些推荐类型可能不会显示或可能显示有限的结果：

- **最近查看的产品**：需要会话数据存储在Cookie/本地存储中。
- **为您推荐**：需要行为数据进行个性化。
- **已购买，已购买**：需要购买历史记录数据。

>[!NOTE]
>
>即使启用了Cookie限制，不依赖行为数据的推荐类型（例如“查看次数最多”和“视觉相似度”）仍可继续正常工作。

## 第三方Cookie同意解决方案

“产品推荐”可能不会自动与第三方Cookie同意解决方案集成。 商家有责任确保数据收集符合适用的隐私法律和法规。

如果您使用自定义Cookie同意解决方案，则可以实施do-not-track Cookie机制来控制数据收集。

### 实施不跟踪Cookie

您可以使用`mg_dnt` Cookie以编程方式控制数据收集：

#### Cookie名称

```javascript
const DNT_COOKIE = "mg_dnt";
```

#### 禁用数据收集

在用户拒绝Cookie时设置do-not-track Cookie：

```javascript
$.mage.cookies.set(DNT_COOKIE, true);
```

#### 启用数据收集

当用户接受Cookie时清除不跟踪Cookie：

```javascript
$.mage.cookies.clear(DNT_COOKIE);
```

## 测试Cookie限制模式

要测试产品Recommendations如何遵守Cookie限制的行为：

1. 在Adobe Commerce配置中启用Cookie限制模式。
1. 不接受Cookie就去你的店面。
1. 验证推荐单元是否显示相应的回退内容。
1. 接受Cookie并确认推荐已开始收集数据。

## 隐私合规

产品推荐数据收集不包括个人身份信息(PII)。 所有用户标识符（如Cookie ID和IP地址）均进行匿名处理。 有关详细信息，请参阅[Adobe隐私政策](https://www.adobe.com/privacy/policy.html)。

>[!TIP]
>
>对于使用数据服务HIPAA扩展的医疗保健客户，可能需要其他配置。 有关详细信息，请参阅[HIPAA准备工作](../data-connection/hipaa-readiness.md)。
