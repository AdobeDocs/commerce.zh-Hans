---
title: 测试和验证
description: 测试和验证有助于确保 [!DNL Payment Services] 功能按预期工作，并为您的客户提供最佳付款选项
exl-id: 95b4615e-73b0-41e8-83e2-e65a0b22f10f
feature: Payments, Checkout, Paas, Saas
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# 测试和验证

在您向购物者公开[!DNL Adobe Commerce]和[!DNL Magento Open Source]的[!DNL Payment Services]之前，最好在沙盒环境&#x200B;_和_&#x200B;中在生产环境中进行测试。 测试和验证有助于确保[!DNL Payment Services]功能按预期工作，并为您的商店和客户提供最佳付款选项。

## 在沙盒环境中测试

在沙盒环境中测试[!DNL Payment Services]是一个重要的验证步骤，即使它是一个仅连接到PayPal沙盒而非实际银行和商家的模拟环境。

1. 使用[信用卡字段](payments-options.md#credit-card-fields)或任何[PayPal付款按钮](payments-options.md#paypal-smart-buttons)成功完成从商店结帐。 有关使用假信用卡进行测试的更多信息，请参阅[测试凭据](#testing-credentials)。
1. 捕获（当您的付款操作为[设置为`Authorize and Capture`](onboard.md#set-payment-services-as-payment-method)时）、[退款](refunds.md)或[void](voids.md)刚刚完成的订单。 如果您的付款操作设置为`Authorize`而不是`Authorize and Capture`，则您也可以[为订单](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice){target="_blank"}创建发票。
1. 在24-48小时内，查看[付款报表](payouts.md)中的交易和其他信息。
1. 在[订单付款状态报告](order-payment-status.md)中查看订单的详细信息。

### 测试凭据

在测试和验证沙盒时，您必须使用虚假信用卡号，这样您就不会对现有信用卡帐户产生真正的费用。

使用PayPal的信用卡生成器[生成随机信用卡信息](https://www.paypal.com/us/smarthelp/article/where-can-i-find-test-credit-card-numbers-ts2157)以进行测试。

要在沙盒模式下测试Apple Pay，请执行以下操作：

* 创建一个[Apple沙盒测试者帐户](https://developer.apple.com/apple-pay/sandbox-testing/#create-a-sandbox-tester-account)，其中包含虚假信用卡和帐单信息。
* [注册沙盒域](https://developer.paypal.com/docs/checkout/apm/apple-pay/#link-registeryoursandboxdomains)。

>[!NOTE]
>
>PayPal的沙盒支付处理有时很慢，该服务偶尔可能会停用。 这种情况不能表明实时产品支付处理的速度和效率。

## 在生产环境中测试

强烈建议您在向购物者公开此功能之前，使用真正的信用卡和银行在生产环境中测试[!DNL Payment Services]。 尽管在沙盒中测试[!DNL Payment Services]很重要，但在生产环境中测试是确保[!DNL Payment Services]按预期工作的最可靠方法。

您可以通过以下两种方式之一在生产环境中测试[!DNL Payment Services]：

* 选择您知道购物者不会下订单的时间。
* 使用购物者暂时无法访问但可供您访问以进行测试的网络商店。

使用真实的信用卡和PayPal帐户完成您的生产测试，测试付款的整个生命周期，包括捕获和退款。 在测试期间完成整个结帐和付款流程，可让您清楚地了解在现场购物者使用您的[!DNL Payment Services]功能时如何工作。

您还应该验证银行对帐单上显示的用于生产测试的支付方式的信息是否正确和符合预期（包括业务描述）。

要在生产模式下测试Apple Pay，您必须[注册您的生产域](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain)。
