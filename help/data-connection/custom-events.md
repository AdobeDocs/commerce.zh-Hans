---
title: 创建自定义事件
description: 了解如何创建自定义事件以将您的Adobe Commerce数据连接到其他Adobe DX产品。
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: db782c0a-8f13-4076-9b17-4c5bf98e9d01
source-git-commit: 81fbcde11da6f5d086c2b94daeffeec60a9fdbcc
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 1%

---

# 创建自定义事件

您可以通过创建自己的店面活动来收集行业独特的数据，从而扩展[事件平台](events.md)。 创建和配置自定义事件时，会将其发送到[Adobe Commerce事件收集器](https://github.com/adobe/commerce-events/tree/main/packages/storefront-events-collector)。

## 处理自定义事件

仅Adobe Experience Platform支持自定义事件。 自定义数据不会转发到Adobe Commerce功能板和量度跟踪器。

对于任何`custom`事件，收集器：

- 添加以`identityMap`作为主标识的`ECID`
- 将`email`作为辅助标识`identityMap`包含在&#x200B;_中，如果在事件中设置了_ `personalEmail.address`
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

仅Experience Platform支持标准事件的属性覆盖。 自定义数据不会转发到Commerce功能板和量度跟踪器。

对于具有`customContext`的任何事件，收集器将覆盖相关上下文中设置的具有`customContext`中字段的联接字段。 覆盖的用例是当开发人员想要重用和扩展由已支持的事件中的页面其他部分设置的上下文时。

### 示例

通过Adobe Commerce Events SDK发布的带覆盖的产品视图：

```javascript
mse.publish.productPageView({
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

在Experience Platform Edge中：

```javascript
{
  xdm: {
    eventType: 'commerce.productViews',
    identityMap: {
      ECID: [
        {
          id: 'ecid1234',
          primary: true,
        }
      ]
    },
    commerce: {
      productViews: {
        value : 1,
      }
    },
    productListItems: [{
        SKU: "1234",
        name: "leora summer pants",
        productCategories: [{
            categoryID: "cat_15",
            categoryName: "summer pants",
            categoryPath: "pants/mens/summer",
        }],
    }],
  }
}
```

基于Luma的商店：

在基于Luma的存储中，发布事件在本机实现。 因此，您可以通过扩展`customContext`来设置自定义数据。

例如：

```javascript
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
```

请参阅[自定义事件覆盖](https://github.com/adobe/commerce-events/blob/main/examples/events/custom-event-override.md)，了解有关处理自定义数据的更多信息。

>[!NOTE]
>
> 使用自定义属性覆盖事件可能会影响默认的Adobe Analytics报表。
