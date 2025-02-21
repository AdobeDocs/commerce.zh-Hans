---
title: 连接Store Fulfillment解决方案
description: 在Adobe Commerce和Store Fulfillment解决方案之间建立连接。 创建和授权Adobe Commerce集成，并将商店履行帐户凭据添加到Adobe Commerce服务配置。
role: Admin, Developer
level: Intermediate
feature: Shipping/Delivery, Install, Configuration, User Account, Tools and External Services
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---

# 连接Store Fulfillment解决方案

通过将所需的身份验证凭据和连接数据添加到Adobe Commerce管理员，将Store Fulfillment Services连接到Adobe Commerce。

- **[配置 [!DNL Commerce integration settings]](#create-an-adobe-commerce-integration)** — 为商店履行服务创建Adobe Commerce集成，并生成访问令牌以验证来自商店履行服务器的传入请求。

- **[配置商店履行服务的帐户凭据](#configure-store-fulfillment-account-credentials)** — 添加凭据以将Adobe Commerce连接到商店履行帐户。

>[!NOTE]
>
>请先完成连接配置并成功验证连接，然后再开始测试。

## 创建Adobe Commerce集成

要将Adobe Commerce与商店履行服务集成，您需要创建Commerce集成并生成可用于对来自商店履行服务器的请求进行身份验证的访问令牌。 您还必须更新Adobe Commerce [!UICONTROL Consumer Settings]选项，以防止从Adobe Commerce向[!DNL Store Fulfillment]服务发出请求时出现`The consumer isn't authorized to access %resources.`响应错误。

1. 在“管理员”中，创建“商店履行”的集成。

   - 命名扩展
   - 输入您的电子邮件地址
   - 输入您的管理员帐户密码

1. 为与以下项的集成配置API资源访问权限：

   - Sales > BOPIS订单更新
   - 系统>商店履行应用程序权限

1. 通过保存和激活集成，生成用于身份验证的访问令牌。

1. 将访问令牌复制并保存到安全的加密位置。

1. 与您的客户经理合作，完成商店履行方面的配置并授权集成。

1. 将Adobe Commerce [!UICONTROL Consumer Settings]选项启用到[!UICONTROL Allow OAuth Access Tokens to be used as standalone Bearer tokens]。

   - 从管理员转到&#x200B;**[!UICONTROL Stores]** > [!UICONTROL Configuration] > **[!UICONTROL Services]** > **[!UICONTROL OAuth]** > **[!UICONTROL Consumer Settings]**

   - 将[!UICONTROL Allow OAuth Access Tokens to be used as standalone Bearer tokens]选项设置为&#x200B;**[!UICONTROL Yes]**。

>[!IMPORTANT]
>
> 集成令牌因环境而异。 如果您使用来自其他环境的源数据还原某个环境的数据库，例如从暂存环境还原生产数据，请从数据库导出中排除`oauth_token`表，以便在还原操作期间不会覆盖集成令牌详细信息。


## 配置存储履行帐户凭据

完成接收表单后，将为您创建一个“沃尔玛商店履行”帐户。 当以下凭据可用时，您将收到这些凭据：

- [!DNL Merchant ID]
- [!DNL Consumer ID]
- [!DNL Consumer Secret]
- [!DNL API Server URL]
- [!DNL Token Auth Server URL] （通常与上述配置相同）

配置和使用“商店履行”需要这些凭据。

>[!NOTE]
>
>帐户创建过程可能需要一些时间才能完成。 在等待凭据时，[查看并配置商店履行解决方案](service-config-settings-overview.md)的其他设置。

### 添加凭据以连接到商店履行

1. 为生产和沙盒环境配置[帐户凭据](enable-general.md)。

1. 从管理员转到&#x200B;**[!UICONTROL Stores > Configuration > Services > Store Fulfillment by Walmart Commerce Technologies]**

1. 输入为&#x200B;**[!UICONTROL Production environment]**&#x200B;提供的帐户凭据。 所有字段都是必填字段。

1. 选择&#x200B;**[!UICONTROL Save Config]**。

1. 通过选择&#x200B;**[!UICONTROL Validate Credentials]**&#x200B;测试连接。

>[!NOTE]
>
>如果凭据无效，请验证您为每个环境输入的值是否正确，然后重新验证。 如果连接时仍有问题，请联系您的客户代表。
