---
title: 创建自定义事件
description: 了解如何创建自定义事件以将您的Adobe Commerce数据连接到其他Adobe DX产品。
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: db782c0a-8f13-4076-9b17-4c5bf98e9d01
TQID: https://experienceleague.adobe.com/D1fAIJRYegeZakCdJLB6F1HME4rUQaeoUjMFNgmqpzs
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 371
ht-degree: 0%

---

# 创建自定义事件

您可以通过创建自己的店面活动来收集行业独特的数据，从而扩展[事件平台](events.md)。 创建和配置自定义事件时，会将其发送到[Adobe Commerce事件收集器](https://github.com/adobe/commerce-events/tree/main/packages/storefront-events-collector)。

## 处理自定义事件

仅Adobe Experience Platform支持自定义事件。 自定义数据不会转发到Adobe Commerce功能板和量度跟踪器。

对于任何`custom`事件，收集器：

- 添加以`ECID`作为主标识的`identityMap`
- 将`email`作为辅助标识&#x200B;_包含在`identityMap`中，如果在事件中设置了_ `personalEmail.address`
- 在转发到Edge之前，将`xdm`对象中的完整事件打包

示例：

通过Adobe Commerce Events SDK发布的自定义事件：

```javascript
mse.publish.custom({
    commerce: {
        saveForLaters: {
            value: 1,
        },
    },
});
```

在Experience Platform Edge中：

```javascript
{
  xdm: {
    identityMap: {
      ECID: [
        {
          id: 'ecid1234',
          primary: true
        }
      ],
      email: [
        {
          id: "runs@safari.ke",
          primary: false
        }
      ]
    },
    commerce: {
        saveForLaters: {
            value: 1
        }
    }
  }
}
```

>[!NOTE]
>
> 使用自定义事件可能影响默认的Adobe Analytics报表。

## 处理事件覆盖（自定义属性）

对于使用`customContext`设置的任何事件集，收集器会覆盖或扩展`custom context`中事件有效负载字段的字段。 覆盖的用例是当开发人员想要重用和扩展由已支持的事件中的页面其他部分设置的上下文时。

仅当转发到Experience Platform时，事件覆盖才适用。 它们不适用于Adobe Commerce和Sensei analytics事件。 Adobe Commerce事件收集器[自述文件](https://github.com/adobe/commerce-events/blob/e34bcfc0deca8d5ac1f9310fc1ee4c1becf4ffbb/packages/storefront-events-collector/README.md)提供了其他信息。

>[!NOTE]
>
>使用Experience Platform事件有效负载中的自定义属性增强`productListItems`时，请使用SKU匹配产品。 此要求不适用于`product-page-view`事件。

### 使用情况

```javascript
const mse = window.magentoStorefrontEvents;

mse.publish.productPageView(customCtx);
```

### 示例1

此示例在发布事件时添加自定义上下文。

```javascript
magentoStorefrontEvents.publish.productPageView({
    productListItems: [
        {
            productCategories: [
                {
                    categoryID: "cat_15",
                    categoryName: "summer pants",
                    categoryPath: "pants/mens/summer",
                },
            ],
        },
    ],
});
```

### 示例2

此示例在发布事件之前添加自定义上下文。

```javascript
const mse = window.magentoStorefrontEvents;

mse.context.setCustom({
  productListItems: [
    {
      productCategories: [
        {
          categoryID: "cat_15",
          categoryName: "summer pants",
          categoryPath: "pants/mens/summer",
        },
      ],
    },
  ],
});

mse.publish.productPageView();
```

### 示例3

此示例在发布者中设置自定义上下文，并覆盖之前在Adobe客户端数据层中设置的自定义上下文。

在此示例中，`pageView`事件在`web.webPageDetails.name`字段中将具有&#x200B;**自定义页面名称2**。

```javascript
const mse = window.magentoStorefrontEvents;

mse.context.setCustom({
  web: {
    webPageDetails: {
      name: 'Custom Page Name 1'
    },
  },
});

mse.publish.pageView({
  web: {
    webPageDetails: {
      name: 'Custom Page Name 2'
    },
  },
});
```

### 示例4

此示例将自定义上下文添加到具有多个产品的`productListItems`事件。

```javascript
const mse = window.magentoStorefrontEvents;

mse.context.setCustom({
  productListItems: [
    {
      SKU: "24-WB01", //Match SKU to override correct product in event payload
      productCategory: "Hand Bag", //Custom attribute added to event payload
      name: "Strive Handbag (CustomName)" //Override existing attribute with custom value in event payload
    },
    {
      SKU: "24-MB04",
      productCategory: "Backpack Bag",
      name: "Strive Backpack (CustomName)"
    },
  ],
});

mse.publish.shoppingCartView();
```

基于Luma的商店：

基于Luma的存储以本机方式实施发布事件，因此您可以通过扩展`customContext`来设置自定义数据。

例如：

```javascript
mse.context.setCustom({
  web: {
    webPageDetails: {
      name: 'Custom Page Name'
    },
  },
});
```

>[!NOTE]
>
> 使用自定义属性覆盖事件可能会影响默认的Adobe Analytics报表。
