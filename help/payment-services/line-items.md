---
title: ' [!DNL Payment Services]的行项目'
description: 了解 [!DNL Payment Services] 的行项目以及如何查看商家仪表板中的行项目。
feature: Payments
role: User
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---

# [!DNL Payment Services]的行项目

[!DNL Payment Services]的行项目是订单中包含的项目。 这些行项目提供如下信息：

* 产品详细信息
* 数量
* 价格（包括税项、折扣及其他相关信息）

此信息对于客户服务、订单管理和正确计费非常有用。

此功能默认对[!DNL Payment Services]启用。 要查看行项目，请执行以下操作：

1. 导航到您的[PayPal商家信息板](https://www.paypal.com/merchant/){target=_blank}。

1. 单击&#x200B;**活动** > **所有事务**。

1. 选择所需订单并查看其行项目：

   > 购物者仪表板视图中的行项目示例

   ![行项目视图](assets/paypal-shopper-dashboard-line-items-view.png){width="500" zoomable="yes"}

## 行项目属性

通过Adobe Commerce下订单时将生成行项目，并且信息会发送到PayPal，具有以下属性：

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `name` | 字符串！ | 项目名称。 如果由于多个数量或税收舍入发放而项目具有多个行，则所有行的项目名称保持不变，但显示的价格可能会因舍入而略有变化。 |
| `unit_amount` | 对象！ | 每单位的物料价格或费率。 包括以下属性： `currency_code`和`value`。 |
| `tax` | 对象 | 每个单位的物料税。 包括以下属性： `currency_code`和`value`。 |
| `quantity` | 字符串！ | 物料数量。 将是一个整数。 |
| `description` | 字符串 | 详细的物料说明。 |
| `sku` | 字符串 | 物料的库存单位（或SKU）。 |
| `url` | 字符串 | 要购买的项目的`URL`。 对买方可见并在买方体验中使用。 |
| `upc` | 对象 | 物料的通用产品代码（或UPC）。 |
| `category` | 字符串 | 物料类别类型。 |

### `unit_amount`属性

`unit_amount`对象包含以下属性：

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `currency_code` | 字符串！ | 用于标识货币的[三字符ISO-4217货币代码](https://developer.paypal.com/api/rest/reference/currency-codes/)。 |
| `value` | 字符串！ | 指示项目的值。 `currency_code`确定所需的小数位数（如果有）。 |

### `tax`属性

`tax`对象包含以下属性：

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `currency_code` | 字符串！ | 用于标识货币的[三字符ISO-4217货币代码](https://developer.paypal.com/api/rest/reference/currency-codes/)。 |
| `value` | 字符串！ | 指示项目的值。 取决于每个`currency_code`是否具有所需的小数位数。 |

### `upc`属性

`upc`对象包含以下属性：

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `type` | 字符串！ | upc类型。 |
| `code` | 字符串！ | 物料的UPC产品代码。 |

+++行项目示例

```json
{
    "name": "Crown Summit Backpack - 1",
    "unit_amount": {
        "currency_code": "USD",
        "value": "38.50"
    },
    "tax": {
        "currency_code": "USD"
        "value": "3.13"
    },
    "quantity": "1",
    "description": "The Crown Summit Backpack is equally at home in a gym locker, study cube or a pup tent, so be sure yours is packed with books,",
    "sku": "24-MB03",
    "url": "https://magento.test/crown-summit-backpack.html",
    "upc": {
        "type": "UPC-A",
        "code": "000003"
    },
    "category": "PHYSICAL_GOODS"
},
{
    "name": "Crown Summit Backpack - 2",
    "unit_amount": {
        "currency_code": "USD",
        "value": "38.50"
    },
    "tax": {
        "currency_code": "USD",
        "value": "3.14"
    },
    "quantity": "1",
    "description": "The Crown Summit Backpack is equally at home in a gym locker, study cube or a pup tent, so be sure yours is packed with books,",
    "sku": "24-MB03",
    "url": "https://magento.test/crown-summit-backpack.html",
    "upc": {
        "type": "UPC-A",
        "code": "000003"
    },
    "category": "PHYSICAL_GOODS"
}
```

+++

有关这些字段及其限制的详细信息，请参阅有关行项目](https://developer.paypal.com/docs/api/orders/v2/#definition-line_item){target=_blank}的[PayPal开发人员文档。

## 管理行项目

Adobe Commerce [根据每行](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/taxes/taxes#warning-messages){target=_blank}的总额计算税额，如果订购了相同项目的多个数量或者在目录中显示含税价格，则可能会导致舍入问题。 在这种情况下，总数量可以拆分为两行，但数量将等于订购的物料总数。

> 贸易商仪表板视图中具有舍入问题的行项目示例

![行项目视图](assets/line-items-example.png){width="600" zoomable="yes"}

+++Adobe Commerce如何计算行项目中的舍入问题

[!DNL Payment Services]的行项目会平衡此舍入问题，以便`unit_amount`或`unit_tax`值对应于订单的总金额。 可以将物料拆分为两行以解决此舍入问题：

* 当舍入问题出现在`unit_amount`上时，商家应该看到此附加行上的价格差异。
* 当舍入问题出现在`unit_tax`上时，单个行项目上不会出现任何差异，因为`tax`未显示在网格中，而是在底部以总计显示。

+++
