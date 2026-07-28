---
title: 客户准备清单
description: 了解如何准备将数据批量迁移到Adobe Commerce as a Cloud Service，其中包含一个准备工作清单，涵盖参与、计算机、源和目标。
feature: Cloud
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目（Adobe管理的SaaS基础架构）。"
role: Developer
level: Intermediate
autotag-review: '2026-07-22T19:19:18.443Z'
TQID: 'https://experienceleague.adobe.com/728hkK-dzIPzyuBhuNyOqEE9FxlVGdVc9R2wIRcXobk'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
subfeature_v2:
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 670b6214b28be93a16130552a226a8cadb487324
workflow-type: tm+mt
source-wordcount: 1171
ht-degree: 0%

---

# 客户就绪性核对清单

{{bulk-data-early-access}}

使用此核对清单以准备使用批量数据迁移工具将数据从[!DNL Adobe Commerce on Cloud]或内部部署实例迁移到[!DNL Adobe Commerce as a Cloud Service]。

迁移工具作为Commerce部署工程(CDE)参与流程的一部分分发。 对该工具的访问权在已签署的CDE协议上被限制，并且它不是公开的。

此清单涵盖共享工具之前需要准备的内容（[阶段1](#stage-1-before-tool-access)），以及在拥有工具后准备开始配置和执行所需的内容（[阶段2](#stage-2-before-running-the-migration)）。 与您的Adobe团队一起尽早查看此核对清单，因为有些项目需要Adobe协调。

## 阶段1：工具访问之前

在提供迁移工具和文档之前，请完成或确认以下操作。

- **CDE参与** — 必须已签署一份Commerce部署工程协议。 在CDE生命周期的交易签署阶段授予工具访问权限。 与您的Adobe团队协调。
- **范围设定调查表已完成** — 在CDE Discovery期间完成范围设定调查表，以验证使用当前工具功能进行迁移是否可行，并评估数据足迹和复杂性。 在继续下一步之前，请确保已经与您的Adobe团队一起完成此操作。
- **未确认HIPAA数据** — 源实例不得包含HIPAA规范的数据。 请在继续之前确认此项。
- **提供的IP地址** — 为您的Adobe团队提供迁移工具将从中运行的静态IP地址列表。 要在Adobe端配置网络访问，需要此项。
- **已设置目标实例** — 必须在迁移开始之前设置目标[!DNL Adobe Commerce as a Cloud Service]实例。 与您的Adobe团队协调以确认实例已就绪。

## 阶段2：运行迁移之前

在有权访问该工具后，请在开始配置和执行之前准备好以下项目。

### 迁移计算机

迁移工具在您控制的计算机（如专用跳转框）上运行。 此计算机必须满足以下要求。

- 已安装&#x200B;**[!DNL Docker]和[!DNL Docker Compose]** — 此工具基于[!DNL Docker]。 `docker`和`docker compose`（或旧版`docker-compose`）都必须安装并在迁移计算机上工作。
- **[!DNL Docker]执行权限** — 必须允许运行迁移的用户执行[!DNL Docker]命令。 在[!DNL Linux]，用户必须属于`docker`组。 在[!DNL macOS]和[!DNL Windows]上，[!DNL Docker Desktop]必须运行并可访问。
- **可写工作目录** — 迁移用户必须完全可写用于提取迁移工具的目录。 该工具在执行期间写入日志、缓存、[!DNL Composer]依赖项和生成的文件。
- **足够的磁盘空间** — 确保有足够的可用磁盘空间用于提取的数据、[!DNL Docker]映像和日志输出。 空间需求因源数据库的大小而异。
- **本地源：从迁移计算机直接连接数据库** — 对于本地源实例，迁移计算机必须具有对源数据库的直接网络访问权限。 该工具不会自动建立本地数据库连接。 在运行任何迁移命令之前，请确认可从迁移计算机访问主机、端口和凭据。
- **已安装云CLI并注册了SSH密钥** — 对于[!DNL Adobe Commerce on Cloud]源实例，迁移计算机上必须安装[云CLI](https://experienceleague.adobe.com/zh-hans/docs/commerce-on-cloud/user-guide/dev-tools/cloud-cli/cloud-cli-overview)。 您还必须在帐户中注册SSH公钥。 有关说明，请参阅[安全连接指南](https://experienceleague.adobe.com/zh-hans/docs/commerce-on-cloud/user-guide/develop/secure-connections)。

### Source实例

- **可访问的Source存储API** — 必须可从迁移计算机访问源存储的REST和GraphQL API。 请确保没有任何HTTP基本身份验证或网络限制会阻止到源URL的API流量。
- **Source OAuth凭据** — 迁移工具使用OAuth对源存储进行身份验证。 在源&#x200B;[!UICONTROL **管理员**] （[!UICONTROL **系统**] > [!UICONTROL **扩展**] > [!UICONTROL Integrations]）中创建或确认集成，并准备好使用者密钥、使用者密钥、访问令牌和访问令牌密钥。
- **PaaS源： Magento Cloud API令牌** — 从&#x200B;[!UICONTROL **帐户设置**] > [!UICONTROL **API令牌**]&#x200B;下的[Cloud帐户设置](https://accounts.magento.cloud)生成[!DNL Cloud]API令牌。 仅当源是[!DNL Adobe Commerce on Cloud]实例时才需要。
- **Source数据库凭据** — （仅限本地）准备好源[!DNL MySQL]数据库连接详细信息以进行配置： `host`、`port`、`user`、`password`和`database`名称。
- **能够暂停cron** — 必须在数据提取期间停止源实例上的cron以防止并发写入。
- **暂停集成和后台作业的功能** — 任何第三方集成(ERP、OMS、PIM)、计划作业或写入源数据库的后台进程都必须暂停提取窗口。
- **启用和禁用维护模式的功能** — （仅限分阶段迁移）如果使用维护窗口运行分阶段迁移，则必须在源实例上启用和禁用维护模式。

### Target实例

- **租户ID和组织ID已确认** — 在配置之前，请从您的Adobe团队中获取您的`TARGET_TENANT_ID`和`TARGET_ORG_ID`。
- **IMS OAuth服务器到服务器凭据** — 迁移工具需要此凭据才能与目标进行身份验证。 通过[Adobe Developer Console](https://developer.adobe.com/console/)生成。 您需要[!UICONTROL Developer]或[!UICONTROL Admin]权限才能访问您的Adobe组织，因为基本用户访问权限不足以创建凭据。 与您的Adobe团队协调以选择正确的产品配置文件，并准备好客户端ID (`ADOBE_IMS_CLIENT_ID`)和客户端密钥(`ADOBE_IMS_CLIENT_SECRET`)。
- **CDMS端点URL** — 由您的Adobe团队提供。 请勿尝试推断此值。 您既需要沙盒和测试迁移的生产前端点，也需要实时直接转换迁移的生产端点。
- **源与目标之间对齐的核心配置** — 该工具不迁移核心配置数据，如存储设置和系统配置。 请在迁移前在目标上手动设置以匹配源。
- **B2B存储：一致配置B2B功能** — 如果源是启用了B2B的存储，请确保在迁移之前在源和目标上一致配置相关的B2B [!UICONTROL Admin]设置。 有关所需的特定设置，请参阅[迁移指南](migration-guide.md)。

### 迁移规划

- **迁移方法已决定** — 在开始之前，确定哪种方法适合您的用例。
  - 单相迁移 — 无需维护模式。 适合在提取期间源可以保持活动状态的任何迁移，例如旱跑、开发或沙盒环境。
  - 多阶段迁移 — 需要维护模式。 生产迁移需要多阶段迁移，其中在提取期间必须冻结源以确保数据一致性。
- **计划的维护时段** — 仅适用于多阶段迁移。 提前规划和沟通维护时段。 在提取和加载阶段的持续时间内，源实例对最终用户不可用。
- **已确认存储视图代码** — 识别源实例上的存储视图代码(`STORE_CODE`)。 它默认为`default`，但必须与[!UICONTROL Admin] > [!UICONTROL Stores] > [!UICONTROL All Stores]中的实际代码匹配。 不正确的存储代码可能会影响迁移期间的数据操作。

确认所有项目后，您就可以使用[迁移服务访问指南](cdms-access.md)验证服务访问权限，然后在[迁移指南](migration-guide.md)中开始配置和执行步骤。
