---
title: 创建自定义事件
description: 了解如何创建自定义事件以将您的Adobe Commerce数据连接到其他Adobe DX产品。
role: Admin, Developer
feature: Personalization, Integration, Eventing
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '260'
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

仅Experience Platform支持标准事件的属性覆盖。 自定义数据不会转发到Commerce功能板和量度跟踪器。

对于具有`customContext`的任何事件，收集器将覆盖相关上下文中设置的具有`customContext`中字段的联接字段。 覆盖的用例是当开发人员想要重用和扩展由已支持的事件中的页面其他部分设置的上下文时。

>[!NOTE]
>
>在覆盖自定义事件时，应该为该事件类型关闭到Experience Platform的事件转发，以避免重复计数。

示例：

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

>[!NOTE]
>
> 使用自定义属性覆盖事件可能会影响默认的Adobe Analytics报表。
