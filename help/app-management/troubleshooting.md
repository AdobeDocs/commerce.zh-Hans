---
title: 疑难解答[!DNL App Management]
description: 解决与应用程序关联、安装、配置和升级有关的常见问题。
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
source-git-commit: a00b9e1654a572e1773b5b7e321683332882d86f
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 0%
---
# 疑难解答[!DNL App Management]

使用以下解决方案可解决与应用程序关联、安装、配置和升级有关的常见问题。

## 在联系应用程序提供商之前

请按照以下解决您的问题的步骤执行操作。 如果您需要应用程序开发人员或提供商的帮助，请收集以下信息：

* 应用程序名称和已安装的版本（如果可从应用程序卡上的&#x200B;**[!UICONTROL Manage]** > **[!UICONTROL Details]**&#x200B;获得）。
* 受影响的Commerce实例和Adobe组织。
* 失败的操作，例如安装或升级，以及失败的步骤。
* 显示的错误消息和故障屏幕快照（如果可用）。
* 故障的大致时间，包括时区。
* 任何重试尝试及其结果。

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

## 安装失败

保持安装页面打开而不刷新，直到安装完成。 关闭或刷新它可能会阻止安装正确完成。

如果安装报告故障：

1. 记下失败的项目和任何显示的错误消息。

1. 检查您是否已完成应用程序的预安装说明。

1. 在再次尝试安装之前，请让应用程序开发人员检查失败的步骤并更正原因。

失败的安装可能会保留应用某些更改。 重试安装后，将跳过记录为成功的自定义步骤；失败或中断的步骤可以再次运行。 要求开发人员检查由部分执行创建的资源。

## 升级失败

升级失败可能会保留部分操作。 请勿作为例行恢复步骤取消关联并重新安装应用程序，因为取消关联会删除配置，并运行破坏性清理脚本。

1. 识别失败的步骤并记录任何显示的错误消息。

1. 要求应用程序开发人员检查日志，检查是否对Commerce或外部资源进行了更改，并更正原因。

1. 在[!DNL App Management]中，选择&#x200B;**[!UICONTROL Retry Upgrade]**。 此操作适用于手动和自动升级模式。

每次重试都会从当前状态创建新计划。 记录为成功的自定义安装步骤将被跳过；失败的或中断的步骤可以再次运行。 在自动模式下，再次部署应用程序也会触发另一次升级尝试。

如果重复尝试失败，请让应用程序开发人员保留运行或尝试ID以及任何执行激活ID，以进行故障排除。 有关状态命令、尝试历史记录和运行时日志，请参阅开发人员文档中的[重试失败的升级](https://developer.adobe.com/commerce/extensibility/app-management/upgrade-app/#retry-a-failed-upgrade){target="_blank"}。

## 升级后资源仍会保留

从应用程序的配置中删除自定义安装步骤时，不会运行其卸载脚本或删除其创建的资源。 升级计划会警告：对于已移除的步骤，不会运行任何脚本，并且升级后的步骤不会出现在进度屏幕或应用程序详细信息中。

要求您的应用程序开发人员确认是否仍需要这些资源，并在需要时提供清理迁移。 有关管理员工作流程，请参阅[升级应用程序](manage-app.md#upgrade-an-app)。

有关技术疑难解答，请参阅[Commerce可扩展性 [!DNL App Management]](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"}以了解更多信息。
