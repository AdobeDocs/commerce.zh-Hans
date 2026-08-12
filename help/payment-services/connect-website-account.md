---
title: 为网站连接其他PayPal帐户
description: 在管理员中完成网站范围内的PayPal载入，将其他PayPal商家帐户连接到单个网站。
role: Admin, User
level: Intermediate
feature: Payments, Checkout, Configuration, Paas, Saas
TQID: 'https://experienceleague.adobe.com/U1zGAU6vYKjk2tc2KXnvyqnYdbA2HKTCNZSKhHdS0Vw'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
source-git-commit: d754c71e287d7d9ff297dd7d95efbaaae7ffc2fc
workflow-type: tm+mt
source-wordcount: 393
ht-degree: 0%

---

# 为网站连接其他PayPal帐户

对于具有&#x200B;**多个网站**&#x200B;的Commerce实例，您可能需要&#x200B;**不同的PayPal商家帐户**。 [!DNL Payment Services]在&#x200B;**全局**&#x200B;上线后启用&#x200B;**网站范围**&#x200B;的PayPal上线。

>[!NOTE]
>
> 此功能仅支持连接新帐户。

## 网站范围内的载入的先决条件

只有当您的商店满足以下要求时，网站级别的载入才可用：

- [Commerce Services Connector](https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/integration-services/saas)安装已完成。
- PayPal帐户已连接到全局（默认配置）范围。

您可以通过检查默认范围中是否填充了以下字段来确认这一点：

- [!UICONTROL Payment Services Sandbox ID]
- [!UICONTROL Payment Services Production ID]
- [!UICONTROL PayPal Merchant ID]

如果这些字段为空，您必须先[完成全局载入](configure-admin.md)。 在完成先决条件之前，**[!UICONTROL Connect different account]**&#x200B;按钮处于禁用状态。

## 启动网站级别的连接

1. 在&#x200B;_管理员_&#x200B;侧边栏中，转到&#x200B;**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**>**[!UICONTROL Sales]**，然后选择&#x200B;**[!UICONTROL Payment Methods]**。
1. 在左上角的范围选择器中，从&#x200B;**[!UICONTROL Default Config]**&#x200B;切换到要载入的&#x200B;**[!UICONTROL Website]**。
1. 单击&#x200B;**[!UICONTROL Connect different account]**。

   如果禁用该按钮，则你的存储区不符合上述[先决条件](#prerequisites-global-scope)。

## 完成载入模式

随即会打开一个弹出窗口。

1. 从下拉菜单中选择您的&#x200B;**[!UICONTROL Country]**。
1. 选择您的载入类型： **[!UICONTROL Basic]**&#x200B;或&#x200B;**[!UICONTROL Advanced]**。
1. 单击&#x200B;**[!UICONTROL Next]**。

>[!NOTE]
>
> 如果您正在匈牙利、西班牙或奥地利上线，则必须打开并查看条款和条件链接，然后才能单击&#x200B;**[!UICONTROL I Accept]**&#x200B;按钮。 在您打开条款和条件之前，该按钮处于禁用状态。

## 登录到PayPal

在您被重定向到PayPal登录页面后，请登录并在PayPal中完成入门培训步骤。

>[!IMPORTANT]
>
> 单击&#x200B;**[!UICONTROL Confirm and Continue]**&#x200B;后，全局范围的会话将结束，网站级别的连接将开始。 如果您意外单击了&#x200B;**[!UICONTROL Connect different account]**，则可以通过选择&#x200B;**[!UICONTROL Cancel]**&#x200B;或在确认之前单击&#x200B;**X**&#x200B;图标来取消。

## 完成并返回管理员

1. 完成PayPal步骤后，关闭PayPal窗口。
1. 单击&#x200B;**[!UICONTROL Finish]**&#x200B;或右上角的&#x200B;**X**&#x200B;关闭入门弹出窗口。
1. Commerce配置页面会自动刷新。

## 确认结果

页面刷新后，在网站范围配置页面中检查：

- 已更新该网站的&#x200B;**[!UICONTROL PayPal Merchant ID]**。
- 显示载入结果的状态标签：

| 状态 | 含义 |
| --- | --- |
| `ACTIVE` | 载入成功完成 |
| `PENDING` | 载入仍在处理中 |
| `ERROR` | 载入未成功完成 |

如果您看到`ERROR`状态，则会显示一条错误消息，说明该问题。 您可以通过再次单击&#x200B;**[!UICONTROL Connect different account]**&#x200B;重试载入流程。
