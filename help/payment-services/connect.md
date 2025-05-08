---
title: 连接实例
description: 使用API密钥和私钥连接您的Commerce实例，并在配置中指定数据空间。
exl-id: 5038fd31-bac5-419e-a172-66919a9b5272
feature: Payments, Checkout, Configuration, Paas
badgePaas: label="仅限PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于云项目(Adobe管理的PaaS基础架构)和内部部署项目上的Adobe Commerce 。"
source-git-commit: 0f2e9c3a7d990a46bafc5f3b8a083436d42643b5
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---


# 连接实例

您使用API密钥和私钥连接Commerce实例，并使用[Commerce Services Connector](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/saas.html)指定配置中的数据空间。 **您只设置一次此连接。**

>[!VIDEO](https://video.tv.adobe.com/v/3447835)

>[!INFO]
>
> 有关其他信息，请参阅我们的[[!DNL Adobe Commerce] 服务连接器](https://experienceleague.adobe.com/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-commerce-services-connector.html?lang=en)视频。

* 如果您&#x200B;*已连接您的实例*，通过获取并使用API凭据并配置Commerce服务，您可以继续[设置测试沙盒](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/sandbox.html)。
* 如果您仍&#x200B;*需要连接实例*，请参阅本主题中有关[获取API凭据](#obtain-api-credentials)和[配置Commerce服务](#configure-commerce-services)的信息。
* 如果您&#x200B;*不确定实例是否已连接*，请导航到&#x200B;**系统** >服务> **Commerce服务连接器**，并查看[!UICONTROL Sandbox Keys]和[!UICONTROL Production Keys]部分中的公共和私有API密钥值，以及[!UICONTROL SaaS Identifier]部分中的&#x200B;*项目*&#x200B;和&#x200B;*数据空间*&#x200B;字段。 如果这些值存在，则表示您的实例已连接。

>[!NOTE]
>
>所有有权使用支付服务的商家都可以使用一个生产数据空间和两个测试数据空间。

## 获取API凭据

要使用Commerce SaaS服务，您必须对沙盒和生产环境使用实例的API密钥(Commerce公共API密钥和私钥)，这些API密钥在[我的帐户信息板](https://account.magento.com/customer/account/login)中创建和管理。 [可以为Commerce帐户创建密钥对](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas)，一个用于沙盒，一个用于生产，但一次只能活动使用一对密钥。

>[!NOTE]
>
>在访问[!UICONTROL My Account]仪表板时需要帮助？ 请参阅[创建Commerce帐户](https://experienceleague.adobe.com/en/docs/commerce-admin/start/commerce-account/commerce-account-create)。

公共API密钥创建后，始终可在“我的帐户”信息板中使用。 您可以根据需要复制或删除它。 在为沙盒或生产环境创建公共API密钥时，私有API密钥将变得可见；它只能从后续对话框中复制或保存，并且以后无法访问。

给定的API密钥对对适用于环境中的所有Commerce服务，因此，如果您已经为您的实例配置了Commerce服务，则Commerce Services Connector中已存在您的API密钥对。

如果您的API密钥丢失，则必须生成一个新的API密钥对[&#128279;](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/connect.html#configure-saas-project)并应用[到Admin中的Commerce Services Connector配置](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/connect.html#generate-an-api-key-and-private-key)和。 如果配置的密钥有误或配置中不存在任何密钥，则付款服务中将显示帐户验证错误对话框，通知您未验证帐户。

查看使用API[&#128279;](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/user-guides/integration-services/saas#availableservices)的可用Commerce服务的列表。

要了解如何为沙盒或生产环境生成API密钥，请参阅[凭据](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/saas.html#apikey)。

>[!IMPORTANT]
>
>建议您不要重新生成API密钥对&#x200B;*和*，请更改活动生产实例上的SaaS标识符和/或数据空间。 如果对实例进行修改，您将丢失实例的数据。

## 配置Commerce服务

可以跨实例使用相同的API密钥，但每个实例必须具有自己的[SaaS数据空间](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/saas.html#saasenv)。

>[!NOTE]
>
>商家必须使用为MageID生成的相同密钥来获取他们的付款权利。

现在您已获得凭据，可以配置SaaS项目和Saas数据空间了。

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]**。
1. 单击&#x200B;**[!UICONTROL Configure Commerce Services]**。

   如果您尚未为帐户配置Commerce服务，则可以看到此选项。

   您将被定向到管理员&#x200B;**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**>**[!UICONTROL Commerce Services Connector]**&#x200B;中的配置区域，以配置您的Commerce服务连接器。

1. 要配置Commerce服务，请按照[SaaS配置](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/integration-services/saas.html#saasenv)中所述的步骤操作。

   >[!INFO]
   >
   > 有关其他信息，请参阅我们的[[!DNL Adobe Commerce] 服务连接器](https://experienceleague.adobe.com/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-commerce-services-connector.html?lang=en#configuration-faqs)视频。

## 端点

[!DNL Payment Services]使用[Commerce Services Connector](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/saas.html)连接到Commerce Services并部署为SaaS。 此[!DNL Commerce Services Connector]通过以下位置的终结点进行通信：

* 沙盒环境的`commerce-beta.adobe.io`。
* `commerce.adobe.io for`用于实时环境。
