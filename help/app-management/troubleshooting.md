---
title: 疑难解答[!DNL App Management]
description: 解决应用程序关联和配置的常见问题。
feature: App Builder, Extensibility, Integration
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 72863f3c-9d27-5dda-afe1-d9f934b1fba0
    internal-label: Extensibility
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
    internal-label: Developer tools
subfeature_v2:
  - id: a743e5dc-8f37-4b5d-a848-03c32ca30598
    internal-label: App Builder
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%
---
# 疑难解答[!DNL App Management]

使用以下解决方案可解决与应用程序关联和配置有关的常见问题。

## 未显示应用程序

如果应用程序在部署后未出现在列表中，请检查以下步骤：

1. 验证应用程序是否已部署并在您的组织中可用。

1. 确认您已登录到Developer Console中的正确Adobe组织。

1. 确保应用程序已准备好连接（您的应用程序开发人员或合作伙伴可以确认）。

如果应用程序仍未显示，请与应用程序开发人员联系或查看[Commerce可扩展性 [!DNL App Management]](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"}文档以了解技术信息。

## 范围同步失败

如果关联应用程序时范围同步失败，请尝试以下操作：

1. 检查您的Commerce实例是否可访问且处于联机状态。

1. 验证您的API凭据是否有效并具有正确的权限。

1. 尝试在应用程序配置中从&#x200B;**[!UICONTROL Manage Scopes]**&#x200B;手动同步。

## 未保存配置

如果配置更改未保存，请尝试以下操作：

1. 检查是否填写了所有必填字段并且这些字段有效。

1. 确保您拥有修改应用程序配置的正确权限。

1. 请尝试刷新页面并再次保存。

如果问题依然存在，请检查浏览器控制台是否存在错误，或者与应用程序开发人员联系。

有关技术疑难解答，请参阅[Commerce可扩展性 [!DNL App Management]](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"}以了解更多信息。
