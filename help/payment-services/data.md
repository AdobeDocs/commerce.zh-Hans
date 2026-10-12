---
title: 可用数据
description: 使用Financial Reporting数据协调报表与非Commerce系统。
role: User
level: Intermediate
exl-id: dbf41ce9-01f9-45d0-b651-e4c499e83822
feature: Payments, Checkout, Data Import/Export, Paas, Saas
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 601e4abe-d9bf-58de-a779-32ed6794dcbe
    internal-label: Data Import/Export
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '167'
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

* [`purchase_unit`，其中`custom_id`和`invoice_id`驻留](https://developer.paypal.com/docs/api/orders/v2/#definition-purchase_unit)
* [显示订单详细信息](https://developer.paypal.com/docs/api/orders/v2/#orders_get)
