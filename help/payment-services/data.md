---
title: 可用数据
description: 使用Financial Reporting数据协调报表与非Commerce系统。
role: User
level: Intermediate
feature: Payments, Checkout, Data Import/Export
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# 可用数据

您可以获得一些订单和付款数据，以便跨外部系统协调Adobe Commerce Financial Reporting。

## 与ERP系统协调

您可以使用与特定订单关联的递增ID，将Adobe Commerce Financial Reporting与非Adobe Enterprise Resource Planning (ERP)系统协调。

当付款服务将Commerce订单发送至PayPal时，增量ID将作为`custom_id` _和_&#x200B;包含在`invoice_id`中（其中还包含在`increment_id`之后的随机字符串）。

在付款的商家活动详细信息和PayPal webhook中均可轻松访问ID。

`invoice_id`和`custom_id`显示在付款的商家活动详细信息底部附近：

商家活动详细信息中的![`custom_id`](assets/merchant-activity-ids.png){width="600" zoomable="yes"}

PayPal webhook详细信息中的`custom_id`和`invoice_id`：

```json
   ...
   {
    "id": "4E855005GK253170H",
    "intent": "AUTHORIZE",
    "status": "COMPLETED",
    "payment_source": {
        ...
    },
    "purchase_units": [
        {
            ...
            "custom_id": "000001322",
            "invoice_id": "000001322-c01bd7c3-920f-4542-a900-738082177e92",
            ...
            "payments": {
                "authorizations": [
                    {
                       ...
                        "invoice_id": "000001322-c01bd7c3-920f-4542-a900-738082177e92",
                        "custom_id": "000001322",
                        ...
                    }
                ],
                "captures": [
                    {
                        ...
                        "invoice_id": "000001322-c01bd7c3-920f-4542-a900-738082177e92",
                        "custom_id": "000001322",
                        ...
                    }
                ]
            }
        }
    ],
    "payer": {
        ...
    },
    "create_time": "2022-09-12T14:59:01Z",
    "update_time": "2022-09-12T14:59:45Z",
    "links": [
        ...
    ]
}
   ...
```

有关更多信息，请参阅PayPal的REST API文档：

* [`purchase_unit`，其中`custom_id`和`invoice_id`位于](https://developer.paypal.com/docs/api/orders/v2/#definition-purchase_unit)
* [显示订单详细信息](https://developer.paypal.com/docs/api/orders/v2/#orders_get)
