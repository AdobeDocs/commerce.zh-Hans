---
title: 设置测试沙盒
description: 使用PayPal沙盒帐户在测试模式下使用 [!DNL Payment Services] 。
exl-id: 99c14b4e-e6cf-48f9-9546-5c0d5c71464d
feature: Payments, Checkout, Configuration, Install, Paas, Saas
source-git-commit: 870c2497a2d6dcfc4066c07f20169fc9040ae81a
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 0%

---

# 设置测试沙盒

在开始沙盒载入之前，您必须注册一个免费的PayPal开发人员帐户，并创建商家（用于入门）和购物者帐户（用于测试您的结帐）。 如果需要，您可以创建多个开发人员帐户。

PayPal沙盒帐户允许您在测试模式下使用[!DNL Payment Services]。 PayPal要求您使用PayPal Developer Portal生成的业务沙盒测试帐户、电子邮件和密码进行沙盒载入。 *在沙盒载入过程中不要创建其他帐户。*

## 沙盒载入

要完成沙盒载入，请执行以下操作：

1. 导航到[PayPal开发人员帐户页面](https://developer.paypal.com/developer/accounts/)。
1. 单击&#x200B;**[!UICONTROL Log in to Dashboard]**&#x200B;并使用您现有的PayPal Developer Portal生成的Business沙盒测试帐户登录，或单击&#x200B;**注册**&#x200B;以创建帐户。
1. 创建PayPal沙盒帐户：
   1. 转到&#x200B;_[!UICONTROL Testing Tools]_>**[!UICONTROL Sandbox Accounts]**。
   1. 单击&#x200B;**[!UICONTROL Create account]**。

      如果您在沙盒PayPal载入过程中创建了PayPal沙盒帐户，则必须[重置载入沙盒](#reset-your-sandbox-account)，因为或者您无法验证电子邮件。

   1. 选择&#x200B;**[!UICONTROL Business]**&#x200B;作为帐户类型，然后单击&#x200B;**[!UICONTROL Create]**。
   1. 在&#x200B;_[!UICONTROL Sandbox Accounts]_部分中，单击您创建的沙盒帐户_[!UICONTROL Manage accounts]_&#x200B;列中的三个圆点。
   1. 单击&#x200B;**[!UICONTROL View/edit account]**。

      ![PayPal — 查看/编辑沙盒帐户](assets/onboarding-viewedit-sandbox.png){width="300" zoomable="yes"}

   1. 复制并保存电子邮件ID和系统生成的密码以供将来使用。

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**。
1. 单击&#x200B;**[!UICONTROL Sandbox onboarding]**。

   如果您尚未完成[!DNL Payment Services]的沙盒载入，则此选项可见。

   沙盒商家ID已自动生成并填充到[设置](configure-admin.md)中。 请勿更改或更改此ID。

   您会看到一个PayPal窗口，用于连接PayPal帐户以开始接受付款。

1. 输入您在步骤3中生成的PayPal沙盒帐户的电子邮件和密码（不是您的PayPal商业帐户信息）以及您所在国家或地区。
1. 单击&#x200B;**[!UICONTROL Next]**。

   ![PayPal — 连接PayPal帐户以进行付款](assets/paypal-connectacct.png){width="300" zoomable="yes"}

1. 使用您之前保存的沙盒帐户凭据继续遵循PayPal流程。
1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**。

   **[!UICONTROL Sandbox onboarding]**&#x200B;按钮不再可见，并且您看到“沙盒付款待处理”文本。

当您的PayPal沙盒载入获得批准时，您应该看到一条通知，表明您的支付系统当前处于沙盒模式并且不处理实时支付。

>[!IMPORTANT]
>
>如果您撤销了对[!DNL Payment Services]和[!DNL Adobe Commerce]的[!DNL Magento Open Source]的同意，以处理您的付款（在您的PayPal帐户设置中），则[!DNL Payment Services]无法处理您商店中的订单。 在您的Payment Services主页上，会显示有关撤销同意的警报。 要关闭警报，请单击&#x200B;**[!UICONTROL Do not show again]**。

### 重置沙盒帐户

如果您在沙盒PayPal新用户引导过程中创建了PayPal沙盒帐户，则必须重置新用户引导沙盒，因为或者您无法验证电子邮件。

要重置沙盒帐户：

1. 单击&#x200B;**[!UICONTROL Reset sandbox]**。 [创建PayPal商业沙盒帐户](https://developer.paypal.com/docs/api-basics/sandbox/accounts/#create-a-business-sandbox-account)。
1. 单击&#x200B;**[!UICONTROL Sandbox onboarding]**&#x200B;并完成下一组步骤。

## 启用联系人电话号码

联系电话号码允许您获取PayPal从客户那里收集的联系电话号码。 PayPal始终从PayPal帐户持有人那里收集联系电话号码，以帮助确认其身份并联系他们以解决其帐户上的问题或完成其履行流程。 但是，PayPal不鼓励直接从商家使用联系电话号码，因为它可能会对销售产生负面影响。 有关详细信息，请参阅[PayPal获取联系电话号码](https://www.sandbox.paypal.com/businessmanage/preferences/website)文档。

默认情况下，此功能为`off`。 启用后，当客户在结账页面之外完成品牌认证结账流程时，商店管理员可以看到电话号码。

>[!IMPORTANT]
>
>此设置不适用于其他签出流。

## 在沙盒环境中测试

强烈建议您先使用测试数据空间实现集成和暂存环境，并使用真正的信用卡和银行在生产环境中测试支付，然后再向购物者公开此功能。

有关详细信息，请参阅[测试和验证](test-validate.md)。
