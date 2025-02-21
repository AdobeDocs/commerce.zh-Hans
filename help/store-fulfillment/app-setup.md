---
title: 应用程序设置
description: 设置 [!DNL Store Assist] 应用程序以管理在线购买、商店订单提货的端到端商店履行工作流和流程。
level: Intermediate
role: Admin
feature: Shipping/Delivery, Configuration, Tools and External Services
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 0%

---

# 应用程序设置

Store Assist是一个由沃尔玛·Commerce技术公司提供支持的“以服务方式履行”(FaaS)平台应用程序。 应用提供商店内履行功能以处理[!DNL buy online, pick up in store] (BOPIS)订单。 借助Store Assist，商店联系人可以查看客户订购的商品，更快地挑选正确的商品，以及设置已履行订单以便向客户进行店内或路边取货交货。

Store Assist应用程序会接收所有订单和客户信息（从订单详细信息到取货时间），并通过移动设备在线提供存储关联的数据。 该应用包括[!UICONTROL Pick]、[!UICONTROL Stage]、[!UICONTROL Handoff]和[!UICONTROL Orders]模块，可帮助商店关联完成以下活动：

- 分配订单交货日期和时间。
- 在客户到达订单提货时收到他们的通知。
- 暂存移交客户的订单。
- 跟踪其分配的商店位置中所有订单的订单状态。

>[!NOTE]
>
>通过查看[应用商店助手履行工作流](store-assist-modules.md)主题，了解有关Store Assist应用的更多信息。

## 配置应用商店助手应用程序

Store Assist应用程序需要两种类型的配置：

- Adobe Commerce管理系统设置，用于[管理客户在登记过程中可用的用户帐户、用户角色、资源权限](user-setup.md)和[汽车制造和模型选择](check-in-experience-setup.md)。

- 前端配置设置用于自定义Store Assist应用程序界面和其他设置，包括：

   - **为Store Assist应用打上品牌印记** — 使用您公司的徽标和颜色自定义应用用户界面。

   - **更新默认说明** — 自定义“商店协助挑选”、“暂存”、“移交”和“订购”模块中的说明，以指导“商店伙伴”完成您公司的履行工作流的每个步骤。

   - **本地化** — 选择应用程序的可用语言。 选择日期和时间格式，然后选择默认度量单位和默认货币。

   - **非活动时间** — 指定应用程序在注销之前必须处于非活动状态的时间量。

   - **从商店取消** — 指定是否可以从商店取消订单以及哪些角色具有取消权限

   - **订单清理窗口** — 指定挑库订单在重新入库之前在暂存中保留的[预计提货提前期](enable-general.md#delivery-method-title-configuration)之后多长时间，例如3天。 默认值为7天。 如果启用此配置，则在此时间到期时自动取消订单。 商品重新上架，商家收到一封取消电子邮件。

   - 自定义所有应用程序内指令（领料、暂存、交货）。

   - **领料通知** — 指定是否在客户下订单后发送推送通知以启动领料流程。

   - **签到通知** — 指定是否在订单签到流程期间发送推送通知 — 签到后、客户等待时间超过指定时间段后。 或者，禁用通知。

   - **交付流程** — 在“商店关联”将订单交付给客户时启用可选流程，例如，需要客户签名或提示关联检查客户ID。

   - **切换时启用项目拒绝** — 允许客户在订单切换期间返回或取消订单项目。

  与Walmart Commerce Technologies客户服务团队合作，完成Store Assist应用程序的前端配置。

## 应用程序下载和安装

设置和配置Store Assist应用程序后，Store Associates可以从其移动设备下载、安装并登录Store Assist应用程序。

- 验证移动设备是否满足商店履行解决方案的[硬件和软件要求](solution-requirements.md#store-assist-app-requirements)。

- 从[Apple App Store](https://apps.apple.com/us/app/store-assist-by-walmart/id1609281539){target="_blank"}或[Google Play应用商店](https://play.google.com/store/apps/details?id=com.walmart.faas.storeassist){target="_blank"}下载Store Assist应用。

- 存储区关联需要以下信息才能登录：

   - 与商店助理帐户关联的&#x200B;**[!UICONTROL Company name]**

   - **存储协助帐户凭据** — 其帐户的用户名和密码凭据。

  Adobe Commerce管理员可以为在“管理商店”设置中启用了[店内提货](merchant-store-configuration.md#pickup-location-configuration)的所有商店位置创建和管理[!DNL Store Assist app]用户帐户。
