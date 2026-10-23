---
title: 过度捕获
description: 了解Payment Services扩展的过度捕获要求和配置。
role: Admin, User
level: Intermediate
feature: Payments, Paas
source-git-commit: d2bcc58f34af50f26d4a4f082e5b3fc30089ab58
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%
---
# 过度捕获

超额捕获允许具有PayPal超额捕获协议的合格商户在开订单发票时捕获超过原始授权金额的金额。 例如，最终金额可能会因基于重量的调整或授权与履行之间的物料成本更改而增加。

PayPal确定每个商户帐户的过度捕获限制。 在[!DNL Payment Services]中启用过度捕获不会建立协议或增加PayPal批准的限制。

>[!NOTE]
>
>本主题介绍[!DNL Payment Services]扩展中的过度捕获。 对于[!DNL Adobe Commerce as a Cloud Service]，请参阅[自定义捕获量](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#custom-capture-amounts)以了解单独的可用性和启用要求。

## 先决条件

在启用过度捕获之前：

* 过度捕获仅在[!DNL Payment Services] 2.17.0或更高版本中可用。
* 过度捕获仅适用于美国企业。 PayPal的[过度捕获要求(PSD2)](https://www.paypal.com/us/cshelp/article/overcapture-requirements-psd2-help954)也适用于向欧洲经济区(EEA)中的PayPal买家出售的美国商家。
* 过度捕获不适用于替代支付方式(APM)。
* 获取与PayPal的过度捕获协议，并通过您的PayPal客户经理确认为您的商户帐户批准的限制。
* 将付款方法的&#x200B;**[!UICONTROL Payment Action]**&#x200B;设置为`Authorize`。 超量捕获适用于稍后在开票期间捕获的授权订单，而不适用于通过`Authorize and Capture`自动捕获的订单。 查看[将 [!DNL Payment Services] 设置为付款方式](production.md#set-payment-services-as-payment-method)。

## 启用过度捕获

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**。
1. 在左侧面板中，展开&#x200B;**[!UICONTROL Sales]**&#x200B;并选择&#x200B;**[!UICONTROL Payment Methods]**。
1. 使用商店范围选择器选择要配置的网站。
1. 展开&#x200B;_[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_部分。
1. 在&#x200B;_[!UICONTROL Payment Services]_部分中，展开_[!UICONTROL General Configuration]_&#x200B;部分。
1. 将&#x200B;**[!UICONTROL Over Capture Enabled]**&#x200B;设置为`Yes`。
1. 单击&#x200B;**[!UICONTROL Save Config]**&#x200B;保存更改。
1. 导航到&#x200B;**[!UICONTROL System]** > **[!UICONTROL Cache Management]**，然后单击&#x200B;**[!UICONTROL Flush Cache]**&#x200B;以刷新所有无效缓存。

## 捕获授权付款

在管理员开具发票期间会发生过度捕获。 请求的捕获金额必须在PayPal为你的商家帐户批准的限制之内。 请参阅[为标准开票工作流创建发票](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice)。

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Orders]**。
1. 打开具有尚未获取的授权付款的订单。
1. 单击&#x200B;**[!UICONTROL Invoice]**。
1. 在自定义捕获量字段中，输入要捕获的总量。 例如，如果授权金额为USD 100，而商定的最终费用为USD 110，请输入`110`，而不是`10`。 请求的金额必须在您的PayPal批准限制之内。
1. 为通过付款提供商请求付款的发票选择联机捕获。
1. 查看发票并单击&#x200B;**[!UICONTROL Submit Invoice]**。

### 使用发票API捕获

使用标准[创建发票](https://developer.adobe.com/commerce/webapi/rest/tutorials/orders/order-create-invoice)终结点：

```http
POST /rest/<store_code>/V1/order/<orderId>/invoice
```

使用订单的存储代码和订单的内部ID。 使用授权的管理员或集成令牌进行身份验证并设置`Content-Type: application/json`。

以下示例有效负荷为已授权使用USD 100的订单请求包含在线捕获USD 110的完整发票，前提是商家的PayPal协议允许该金额：

```json
{
  "capture": true,
  "notify": false,
  "arguments": {
    "extension_attributes": {
      "custom_capture_amount": 110
    }
  }
}
```

在此示例中：

1. `capture`请求联机捕获。
1. `notify`控制Commerce是否发送发票通知电子邮件。
1. `custom_capture_amount`是要捕获的最终数量，而不是超过授权数量的增加。

## 对拒绝的捕获进行故障排除

如果PayPal拒绝过度捕获请求：

* 确认用于付款的PayPal商家帐户存在过度捕获协议。
* 检查请求的金额是否在批准的限制之内。 如果超过限额，请要求降低限额或联系您的PayPal客户经理讨论提高限额。
