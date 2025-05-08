---
title: 退款
description: 在贷项通知单流程中，为管理员中的 [!DNL Payment Services] 订单创建退款。
exl-id: 2b3721a1-9c9d-4e3f-ab7d-5bd61573dcb4
feature: Payments, Checkout, Paas, Saas
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# 退款

在管理员中创建[!DNL Payment Services]订单的退款作为贷项通知单流程的一部分。 贷项通知单是一种文档，它显示应付给客户的全部或部分退款的金额，可用于购买或直接退款给客户。 只能为[开票](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice){target="_blank"}的订单签发贷项通知单。

请参阅我们的核心用户指南中的[贷项通知单](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memos){target="_blank"}，了解更多信息以及如何发放和打印贷项通知单。

对于使用PayPal或信用卡处理的订单，您可以：

* 退回订单的全部金额
* 退回订单的部分金额（或多个部分金额）
* 退款金额小于特定订单项目的值

有关详细信息，请参阅我们的核心用户指南中的[发出贷项通知单](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memo-create){target="_blank"}。

>[!NOTE]
>
>如果您尝试对超过剩余订单金额（原始金额减去现有退款总额）的订单进行部分退款，或者您发出的退款金额大于全部订单金额，则PayPal或信用卡处理的订单会发生错误。

您的[!UICONTROL Payment Settings]配置中的[!UICONTROL Payment Action]设置（`Authorize`或`Authorize and Capture`）决定了订单的[基本退款工作流](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memos#refund-workflow){target="_blank"}。

有关详细信息，请参阅&#x200B;_发出贷项通知单_&#x200B;的[付款操作设置部分](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memo-create#payment-action-setting){target="_blank"}。
