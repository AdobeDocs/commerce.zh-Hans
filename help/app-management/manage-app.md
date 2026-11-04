---
title: 管理您的应用程序
description: 关联、安装、配置、升级和取消App Builder应用程序与Commerce实例的关联。
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
source-wordcount: '1240'
ht-degree: 0%
---

# 管理您的应用程序

使用[!DNL App Management]将App Builder应用程序与您的Commerce实例关联、安装、配置、升级和取消关联。 配置表单从每个应用程序的架构生成，因此无需自定义管理员UI开发即可管理设置。

![应用管理](assets/app-management-view.png){width="500" zoomable="yes"}

## 在管理员中查找应用程序

在&#x200B;**[!UICONTROL Apps]** > **[!UICONTROL App Management]**&#x200B;下，每个应用程序都显示为卡片。 该列表可包含与所选Adobe IMS组织的Adobe Commerce实例关联的每个应用程序。 使用信息卡上方的控件来缩小结果范围：

| 控件 | 描述 |
| --- | --- |
| **[!UICONTROL Filter by app...]** | 按应用程序名称搜索。 |
| **[!UICONTROL Status]** | 按生命周期状态限制卡片。 **[!UICONTROL All Statuses]**&#x200B;显示每个应用；其他值包括&#x200B;**[!UICONTROL Associated]**、**[!UICONTROL Installed]**、**[!UICONTROL Partially Installed]**&#x200B;和&#x200B;**[!UICONTROL Unassociated]**。 每张信息卡上的状态与列表中的彩色指示器匹配。 |
| **[!UICONTROL Extensibility patterns]** | 根据应用程序使用的功能限制信息卡。 **[!UICONTROL All Extensibility Patterns]**&#x200B;显示每个应用；其他值与每个卡片上的徽章一致，如&#x200B;**[!UICONTROL Business Configuration]**、**[!UICONTROL Admin UI SDK]**、**[!UICONTROL Webhooks]**&#x200B;和&#x200B;**[!UICONTROL Events]**。 |

搜索字段和两个筛选器一起应用。 要再次显示完整列表，请清除搜索字段并选择&#x200B;**[!UICONTROL All Statuses]**&#x200B;和&#x200B;**[!UICONTROL All Extensibility Patterns]**。

### 查看应用程序详细信息

在应用程序的卡片上，选择&#x200B;**[!UICONTROL Manage]** > **[!UICONTROL Details]**&#x200B;以查看其名称、描述和版本。 该对话框提供两个选项卡：

* **[!UICONTROL Details]**&#x200B;列出了应用程序的业务用例，包括事件和自定义安装步骤。 查看标签和描述，了解应用程序向Commerce添加的内容。
* **[!UICONTROL App config]**&#x200B;将应用程序的配置显示为JSON以供检查。

显示应用程序业务用例的![详细信息选项卡](assets/application-details.png){width="600" zoomable="yes"}

![显示应用程序JSON配置的“应用程序配置”选项卡](assets/app-config.png){width="600" zoomable="yes"}

## 获取应用程序

**[!UICONTROL Acquire App]**&#x200B;打开[Adobe Exchange](https://exchange.adobe.com/apps/browse/ec){target="_blank"}的新浏览器选项卡（或单独的浏览器视图），您可以在其中发现与Commerce相关的市场列表并将应用程序添加到您的Adobe IMS组织。 获取、批准和部署应用程序后，应用程序将出现在[!DNL App Management]中，以显示[关联](#associate-an-app)和[安装](#install-an-app)。

## 先决条件

在关联应用程序之前，请确保您满足以下条件：

| 要求 | 描述 |
| --- | --- |
| **管理员访问权限** | 具有[!DNL App Management]权限的Commerce管理员 |
| **已部署应用程序** | App Builder应用程序已部署到您的组织并准备好连接 |
| **组织访问权限** | 访问部署应用程序的Adobe组织 |

## 教程

观看本视频，了解如何将应用程序与Commerce实例关联并配置设置。

>[!VIDEO](https://video.tv.adobe.com/v/3478965?captions=chi_hans)

## 关联应用程序

关联过程将从Commerce导入网站、商店和商店视图，并在应用程序和Commerce实例之间创建链接。

要将App Builder应用程序链接到Commerce实例，请执行以下操作：

1. 导航到&#x200B;**[!UICONTROL Apps]** > **[!UICONTROL App Management]**。

1. 单击&#x200B;**[!UICONTROL Associate App]**。

   ![关联应用](assets/associate-app.png){width="500" zoomable="yes"}

1. 从列表中选择&#x200B;**[!UICONTROL Project]**。

1. 选择&#x200B;**[!UICONTROL Workspace]**。

1. 单击&#x200B;**[!UICONTROL Associate]**。

   ![应用详细信息](assets/app-details.png){width="500" zoomable="yes"}

>[!WARNING]
>
>如果范围同步失败，则关联仍会完成。 您可以稍后从关联应用程序配置的&#x200B;**[!UICONTROL Manage Scopes]**&#x200B;视图中手动同步作用域。

## 安装应用程序

关联可将应用程序链接到您的Commerce实例。 对于包含可安装组件（如事件、Webhook、管理员UI扩展或自定义安装步骤）的应用程序，安装会将这些组件应用于实例。

1. 在[!DNL App Management]中打开关联应用程序的安装对话框。

1. 查看应用程序的业务用例和列出的安装步骤。

1. 如果显示&#x200B;**[!UICONTROL Pre Installation Instructions]**，请先完成这些先决条件，然后再继续。

   ![包含预安装说明和业务使用案例的安装审查](assets/installation-review.png){width="600" zoomable="yes"}

1. 单击&#x200B;**[!UICONTROL Install]**。

1. 监视各个项目的进度指示器，直到安装完成。

   ![单个项目的安装进度](assets/installation-progress.png){width="600" zoomable="yes"}

   >[!WARNING]
   >
   >保持页面处于打开状态，直到安装完成。 关闭或刷新页面可能会阻止正确完成安装。

1. 验证是否显示&#x200B;**[!UICONTROL Successfully Installed]**&#x200B;以及已完成项目是否带有复选标记。

   ![成功安装已完成项目，并带有复选标记](assets/installation-success.png){width="600" zoomable="yes"}

1. 完成应用程序提供的任何安装后说明，然后[根据需要配置其设置](#configure-settings)。

## 配置设置

在[!DNL App Management]视图中关联应用程序后，通过表单配置其设置：

1. 在关联应用的卡片上，选择&#x200B;**[!UICONTROL Manage]** > **[!UICONTROL Configure]**。

该表单会显示应用程序的可配置设置。

1. 根据需要修改值。

1. 单击&#x200B;**[!UICONTROL Save]**。

### 特定于范围的配置

当不同的网站、商店或商店视图需要唯一的设置时，请使用特定于范围的配置。 例如，仅为特定区域或商店视图启用某个功能，或者为每个品牌使用不同的设置。 较低作用域的设置将覆盖较高作用域的设置。

要覆盖特定范围级别的全局值，请执行以下操作：

1. 单击&#x200B;**[!UICONTROL Change Scope]**。

1. 从列表中选择一个范围。

1. 修改此范围的值。

1. 单击&#x200B;**[!UICONTROL Save]**。

## 管理范围

从应用程序详细信息屏幕访问&#x200B;**[!UICONTROL Manage Scopes]**&#x200B;以管理应用程序的范围层次结构。

![管理作用域](assets/manage-scopes.png){width="500" zoomable="yes"}

| 操作 | 描述 |
| --- | --- |
| **[!UICONTROL Add root scope]** | 添加仅适用于应用程序的范围。 |
| **[!UICONTROL Sync Commerce scopes]** | 在添加或更改网站、商店和商店后，从Commerce中刷新它们视图的列表。 |
| **[!UICONTROL Import scopes]** | 从文件批量导入作用域。 |

## 升级应用程序

当应用程序开发人员部署已安装应用程序的新版本时，[!DNL App Management]会收到升级可用通知。 App Builder部署和应用程序管理升级是单独的操作：升级会将计划的更改应用于已安装的组件，例如事件、webhook和管理UI扩展。

请让您的应用程序开发人员确认该应用程序是否支持升级。 有关SDK先决条件和迁移要求，请参阅开发人员文档中的[升级您的应用程序](https://developer.adobe.com/commerce/extensibility/app-management/upgrade-app/){target="_blank"}。

### 查看并开始升级

在手动模式（默认）中，您将在[!DNL App Management]中查看并开始升级。

1. 记录已安装的应用程序版本和配置，并在应用程序开发人员的帮助下备份应用程序数据和外部资源。

1. 导航到&#x200B;**[!UICONTROL Apps]** > **[!UICONTROL App Management]**&#x200B;并打开应用程序的可用升级。

1. 查看计划的更改和任何警告。 升级可以添加、修改或删除组件。 如果删除自定义安装步骤，则不会运行其卸载脚本，也不会自动清理该步骤创建的资源。 在继续之前，请与应用程序开发人员确认任何所需的清理。

1. 开始升级并监视列出的操作的进度。

1. 查看升级结果并检查是否有失败的操作。 如果升级失败，请在使用&#x200B;**[!UICONTROL Retry Upgrade]**&#x200B;之前执行[升级失败](troubleshooting.md#upgrade-fails)。

在手动模式下，在开始升级之前，不会应用对已安装的Commerce组件进行的计划更改。 但是，部署可以更新已安装的应用程序在升级运行之前已使用的运行时操作代码。

### 自动升级

您的应用程序开发人员可控制升级模式。 要求开发人员确认应用程序是使用手动还是自动升级。

>[!WARNING]
>
>自动升级是实验性的，在部署后启动，无需管理员审核，包括可修改外部资源的自定义安装脚本。 在启用自动升级之前（包括新部署的版本将模式从手动更改为自动）与您的开发人员进行协调。

### 业务配置更改

对应用程序业务配置架构所做的更改会在部署后自动显示。 它们与安装和升级分开，不会触发应用程序升级。

## 取消与应用程序的关联

当您不再需要某个应用程序连接到Commerce实例时，请取消该应用程序的关联。 例如，您可能需要停用集成、切换到其他工作区或清理测试配置。

>[!WARNING]
>
>取消关联将删除此实例的所有配置值。 无法撤消此操作。 卸载还可以通过自定义卸载脚本删除应用程序组件和资源。

继续操作之前，请记录已安装的版本和配置，备份应用程序数据，并询问应用程序开发人员要移除哪些应用程序卸载脚本资源以及哪些资源需要手动清理。 计划任何服务中断以及如何恢复应用程序、其设置和数据。 对于例行更新，请[升级应用程序](#upgrade-an-app)，而不是取消关联。

要从Commerce实例中删除应用程序：

1. 导航到&#x200B;**[!UICONTROL Apps]** > **[!UICONTROL App Management]**。

1. 在应用程序的卡片上，选择&#x200B;**[!UICONTROL Manage]** > **[!UICONTROL Unassociate]**。

1. 查看列出的业务用例和受卸载影响的组件，包括事件和自定义安装步骤。

   ![取消关联确认列表受影响的业务用例](assets/unassociate-app.png){width="600" zoomable="yes"}

1. 确认操作。

## 相关文档

* [故障排除 [!DNL App Management]](troubleshooting.md) — 解决关联、安装、配置和升级等常见问题。
* [升级您的应用程序](https://developer.adobe.com/commerce/extensibility/app-management/upgrade-app/){target="_blank"} — 开发人员对升级模式、迁移脚本和诊断的要求。
