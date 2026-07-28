---
title: 运行批量数据迁移
description: 了解如何使用CLI配置并运行从Adobe Commerce PaaS或内部部署实例到Adobe Commerce as a Cloud Service的批量数据迁移。
feature: Cloud
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目（Adobe管理的SaaS基础架构）。"
role: Developer
level: Intermediate
autotag-review: '2026-07-22T19:19:07.600Z'
TQID: 'https://experienceleague.adobe.com/z9659Vnf2JLxJ4U5p3tEEjurj5Mg3bfKj68Gheq2AXY'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
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
source-wordcount: 2802
ht-degree: 0%

---

# 运行批量数据迁移

{{bulk-data-early-access}}

本指南是一个分步操作参考，介绍了如何使用批量数据迁移工具将数据从[!DNL Adobe Commerce] PaaS或内部部署安装迁移到[!DNL Adobe Commerce as a Cloud Service]。 实际配置值和特定于环境的详细信息因您的设置而异。

在开始之前，请确认您已完成[客户准备工作清单](readiness-checklist.md)中的每个项目，并通过[迁移服务访问指南](cdms-access.md)验证API访问。

>[!NOTE]
>
>作为工具分发包的一部分，提供了涵盖该工具的架构、内部设计、数据转换框架和完整性测试框架的综合技术文档。

## 先决条件

- 必须在运行迁移的计算机上安装&#x200B;**[!DNL Docker]**&#x200B;和&#x200B;**[!DNL Docker Compose]**。
- 运行迁移的用户必须具有执行`docker`和`docker compose` （或旧版`docker-compose`）命令的权限。 在[!DNL Linux]，用户必须属于`docker`组。 在[!DNL macOS]和[!DNL Windows]上，[!DNL Docker Desktop]必须运行并可访问。 迁移CLI重复调用[!DNL Docker]，此处出现的权限错误会阻止运行。
- 在运行迁移之前，源系统和目标系统之间的核心配置必须一致。 此工具不会迁移核心配置数据，例如存储设置和系统配置。 请在目标系统上单独设置它，并在迁移之前使其与源系统保持一致。

## 设置工具包

设置批量数据迁移的环境：

>[!VIDEO](https://video.tv.adobe.com/v/3496121)

1. 提取`ccsaas-migration-tools.tar.gz`的内容。

1. 从提取的`ccsaas-migration-tools`文件夹运行所有命令，其中`bin/console`位于该文件夹中。

1. 确保该文件夹对于日志、缓存、[!DNL Composer]和生成的文件是可写的。

   将该目录下所有文件和子文件夹的所有权更改给运行迁移的操作系统用户，以便该工具可以一致地读取和写入。 例如，在[!DNL Linux]上： `chown -R <user>:<group> <project-root>`。

1. 通过复制示例文件（`.example.env`到`.env`和`.my.cnf.example`到`.my.cnf`）在项目根中创建`.env`和`.my.cnf`文件，然后填写以下部分中描述的值。

### 示例配置文件

存储库根目录中的`.example.env`和`.my.cnf.example`文件是配置的起点。 将每个文件复制到其工作名称并填充所需的值。

| 示例文件 | 复制到 | 涵盖的内容 |
| --- | --- | --- |
| `.example.env` | `.env` | 所有受支持的环境变量的注释列表：性能、CDMS、IMS、目标SaaS、源URL身份验证、OAuth和可选PaaS值（`.my.cnf`中设置`id=`时`MAGENTO_CLOUD_CLI_TOKEN`）。 `.env`文件中提供了完整的变量列表。 |
| `.my.cnf.example` | `.my.cnf` | 为本地[!DNL MySQL]和PaaS (`id=project:environment`)引用`[section]`布局。 `[section]`名称必须与`.env`中的`SOURCE_CONNECTION_NAME`匹配。 针对PaaS的字段包括`user`、`password`、`host`、`port`、`database`和`id=`。 |

## 配置环境文件

项目根目录中的`.env`文件是迁移和提取配置。 它驱动CLI管道，包括源和目标URL、OAuth、远程CDMS连接、SaaS和IMS身份验证以及其他开关。

>[!NOTE]
>
>请勿在URL中包含结尾斜杠。 例如，使用`https://example.com`而不是`https://example.com/`。

编辑`.env`文件并正确设置至少以下值。 有关支持的变量的完整列表，请参阅`.example.env`中的内联注释。

```shell-session
SOURCE_INSTANCE_URL=https://<source-host>
SOURCE_INSTANCE_GRAPHQL_URL=https://<source-host>/graphql
SOURCE_INSTANCE_REST_URL=https://<source-host>/rest
SOURCE_INSTANCE_CONSUMER_KEY=<consumer_key>
SOURCE_INSTANCE_CONSUMER_SECRET=<consumer_secret>
SOURCE_INSTANCE_ACCESS_TOKEN=<access_token>
SOURCE_INSTANCE_ACCESS_TOKEN_SECRET=<access_token_secret>
```

### 配置源OAuth凭据

>[!VIDEO](https://video.tv.adobe.com/v/3496142)

这四个值表示从迁移工具到源存储API的请求。 若要获取它们，请打开源[!UICONTROL Admin]，然后转到&#x200B;[!UICONTROL **系统**] > [!UICONTROL **扩展**] > [!UICONTROL **集成**]。 创建或打开集成，然后将值复制到`.env`：

```shell-session
SOURCE_INSTANCE_CONSUMER_KEY=<consumer_key>
SOURCE_INSTANCE_CONSUMER_SECRET=<consumer_secret>
SOURCE_INSTANCE_ACCESS_TOKEN=<access_token>
SOURCE_INSTANCE_ACCESS_TOKEN_SECRET=<access_token_secret>
```

### 设置云CLI令牌

>[!NOTE]
>
>这仅适用于[!DNL Adobe Commerce on Cloud]源实例。 该工具自动从`.my.cnf`中检测源类型。 如果`SOURCE_CONNECTION_NAME`节包含`id=`行（例如，`id=project:production`），则源是[!DNL Adobe Commerce on Cloud]，需要`MAGENTO_CLOUD_CLI_TOKEN`。 对于没有`id=`的内部部署源，不需要此令牌，并跳过通道设置。

1. 转到`https://accounts.magento.cloud`并登录。

1. 单击您的配置文件图像，然后选择&#x200B;[!UICONTROL **帐户设置**]。

1. 转到&#x200B;[!UICONTROL **API令牌**]&#x200B;部分。

1. 选择&#x200B;[!UICONTROL **创建API令牌**]，为其提供描述性名称，并复制生成的令牌。

1. 在`.env`中设置令牌：

   ```text
   MAGENTO_CLOUD_CLI_TOKEN=<your_magento_cloud_api_token>
   ```

>[!NOTE]
>
>如果这是您第一次使用Cloud CLI，则还必须将SSH公钥添加到您的帐户。 有关说明，请参阅[安全连接指南](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/secure-connections)。

### 调整Commerce管理设置

在迁移之前，请确保源和目标之间的以下设置一致。

>[!NOTE]
>
>为确保顺利迁移，[!DNL Adobe]建议您使目标实例中的所有核心配置与源一致。

### 配置目标SaaS和IMS凭据

>[!VIDEO](https://video.tv.adobe.com/v/3496167)

这些是目标的[!DNL Adobe Commerce as a Cloud Service] IMS和API设置。 您需要环境的租户ID、组织ID、IMS OAuth服务器到服务器凭据以及正确的IMS主机。 与您的Adobe团队协调以访问组织、租户和配置文件。 请勿尝试推断或估计敏感值。

#### 生成IMS凭据

使用[Adobe Developer Console](https://developer.adobe.com/console/)。 您需要Adobe组织上的[!UICONTROL Developer]或[!UICONTROL Admin]访问权限才能创建项目。 基本用户登录不足以添加API。

1. 创建一个项目或打开一个现有项目，然后选择[!UICONTROL Add API]。

1. 选择&#x200B;[!UICONTROL **Adobe Commerce as a Cloud Service**]&#x200B;并继续。

1. 选择&#x200B;[!UICONTROL **OAuth服务器到服务器**]&#x200B;作为身份验证类型并继续。

1. 选择您的Adobe团队希望此租户使用的产品配置文件，然后选择&#x200B;[!UICONTROL **保存配置的API**]。

1. 在项目侧边栏中，打开&#x200B;[!UICONTROL **OAuth服务器到服务器**]（或&#x200B;[!UICONTROL **凭据**]），然后将客户端ID和客户端密钥作为`ADOBE_IMS_CLIENT_ID`和`ADOBE_IMS_CLIENT_SECRET`复制到`.env`中。

IMS令牌终结点(`ADOBE_IMS_URL`)必须与凭据的环境匹配。

| 层 | 典型`ADOBE_IMS_URL` |
| --- | --- |
| QA或暂存 | `https://ims-na1-stg1.adobelogin.com` |
| 预生产或生产 | `https://ims-na1.adobelogin.com` |

>[!NOTE]
>
>这些URL中的`na1`表示配置目标实例的区域。 如果您的实例配置在不同的区域，请将其替换为相应的区域标识符。

`ADOBE_IMS_META_SCOPES`必须匹配在该凭据上设置的作用域。 `.example.env`文件包含完整的逗号分隔范围字符串作为引用。 仅当Adobe指示您进行更改时，才应更改此设置。

#### 将[!DNL Adobe I/O]凭据映射到环境文件

在[!DNL Developer Console]中，OAuth服务器到服务器值显示为客户端ID和客户端密钥，对应于以下JSON结构：

```json
{
  "client_id": "xxxxxxxxxxxxxxxxxxxxxxxxxxx",
  "client_secret": "xxxxxxxxxxxxxxxxxxxxxxxxxxx"
}
```

将它们映射到`.env`（占位符示例）：

```shell-session
TARGET_ORG_ID=<org_id>@AdobeOrg
ADOBE_IMS_URL=https://ims-na1.adobelogin.com
ADOBE_IMS_CLIENT_ID=xxxxxxxxxxxxxxxxxxxxxxxxxxx
ADOBE_IMS_CLIENT_SECRET=xxxxxxxxxxxxxxxxxxxxxxxxxxx
ADOBE_IMS_META_SCOPES=AdobeID,openid,additional_info.projectedProductContext
```

SaaS API主机在生产前和生产中有所不同。 `TARGET_INSTANCE_REST_URL`和`TARGET_INSTANCE_GRAPHQL_URL`必须使用与迁移相同的Commerce API环境，即预生产环境或生产环境。 不要将一个层与另一层的CDMS或租户混合。

| 环境 | `TARGET_INSTANCE_*_URL`中的典型主机 |
| --- | --- |
| 预生产或沙盒 | `https://na1-sandbox.api.commerce.adobe.com/{tenantId}` |
| 生产 | `https://na1.api.commerce.adobe.com/{tenantId}` |

>[!NOTE]
>
>这些URL中的`na1`表示配置目标实例的区域。 如果您的实例配置在不同的区域，请将其替换为相应的区域标识符。

```shell-session
TARGET_TENANT_ID=<tenant_id>
TARGET_ORG_ID=<org_id>@AdobeOrg
ADOBE_IMS_URL=https://ims-na1.adobelogin.com
ADOBE_IMS_CLIENT_ID=<client_id>
ADOBE_IMS_CLIENT_SECRET=<client_secret>
ADOBE_IMS_META_SCOPES=AdobeID,openid,additional_info.projectedProductContext
TARGET_INSTANCE_REST_URL=https://na1-sandbox.api.commerce.adobe.com/{tenantId}
TARGET_INSTANCE_GRAPHQL_URL=https://na1-sandbox.api.commerce.adobe.com/{tenantId}/graphql
```

对于生产SaaS主机，请将`TARGET_INSTANCE_*` URL中的`na1-sandbox`替换为`na1`。 对该层使用匹配的`ADOBE_IMS_URL`，如上表所示。

### 设置CDMS端点

将迁移工具指向与要迁移到的环境匹配的CDMS API主机。 在`.env`中设置`CDMS_HOST`（通常为`CDMS_PORT=443`）。 使用一台主机（预生产或生产），而不是同时使用两者。

| 环境 | 使用时间 | `CDMS_HOST` |
| --- | --- | --- |
| 预生产 | 生产前运行或沙盒样式运行，非生产CDMS | `https://commerce-data-migration-service-preprod-external.adobe.io` |
| 生产 | 实时生产迁移或直接转换 | `https://commerce-data-migration-service-prod-external.adobe.io` |

设置或取消注释与运行匹配的块：

```shell-session
# Pre-production CDMS
CDMS_HOST=https://commerce-data-migration-service-preprod-external.adobe.io
CDMS_PORT=443

# Production CDMS (use for prod cutover only)
# CDMS_HOST=https://na1.api.commerce.adobe.com
# CDMS_PORT=443
```

### 设置商店代码

`STORE_CODE`是迁移工具用于源实例REST API调用、综合测试客户创建和数据清理的存储视图代码。 在加载阶段还会作为`x-store-code`标头发送。

`STORE_CODE`在`.example.env`中默认为`default`。 验证它是否与源实例的默认存储视图代码匹配。 若要查看，请在源[!UICONTROL Admin]中转到&#x200B;[!UICONTROL **商店**] > [!UICONTROL **所有商店**]，然后查看&#x200B;[!UICONTROL **代码**]&#x200B;列以了解应使用的商店视图。 如果显示的代码没有`default`，请更新`.env`中的`STORE_CODE`以匹配。

## 配置数据库连接文件

>[!VIDEO](https://video.tv.adobe.com/v/3496152)

`.my.cnf`文件为迁移工具的提取端提供[!DNL MySQL]连接设置。 通过将`.my.cnf.example`复制到项目根目录中的`.my.cnf`来创建它。 分区名称必须与`.env`中的`SOURCE_CONNECTION_NAME`匹配。

对于内部部署或自托管源：

```ini
[<connection-name>]
user=<db_user>
password='<db_password>'
host=<db_host>
port=3306
database=<db_name>
```

>[!NOTE]
>
>运行迁移工具的计算机必须具有对源数据库的直接网络访问权限。 该工具不会自动建立或验证内部部署连接。 在运行任何迁移命令之前，请确认可从迁移计算机访问主机、端口和凭据。

对于[!DNL Adobe Commerce on Cloud]源：

```ini
[<connection-name>]
id=<project_id>:<environment>
```

`id=`字段告知工具源是PaaS，并使用`MAGENTO_CLOUD_CLI_TOKEN`触发通道设置。 `project_id`和`environment`值在[!DNL Cloud Console]中或通过`magento-cloud project:list`和`magento-cloud environment:list`命令提供。

## 准备网络和实例

商店前面的HTTP基本身份验证可以阻止API和工具流量。 请确保为迁移使用的源URL禁用了该设置，或者允许该工具的路径，以便REST和GraphQL请求可以到达存储区。

### 在提取期间维护源数据库的稳定性

虽然该工具会从源数据库提取数据，但其他进程都不应写入源数据库。 并发写入可能会导致快照不一致。

- 停止源上的cron，以及运行`bin/magento`或其他写入程序的任何操作系统计划程序（对于提取窗口），或确保它们在提取期间无法运行。
- 查看其他集成，例如ERP、OMS、PIM、自定义作业和写入同一数据库的第三方API。 暂停或阻止对提取窗口的写入，以便在提取运行时没有任何内容会更改表。
- 这补充了维护模式和通道或数据库访问。 它们一起减少了店面和API流量。 Cron和集成是单独的写入源，您必须显式控制这些写入源。

### 目标

如果必须在迁移之前清除目标目录，请以小批量（例如一次删除200个）删除[!UICONTROL Admin]中的产品，以避免重复目录冲突和批量删除超时。

## 构建并运行迁移

从具有写入权限的提取项目目录工作。

### 通过SSH使会话保持活动状态

如果通过SSH进行连接，则断开的网络可能会终止外壳并中断长时间的迁移。 GNU `screen`命令使会话在服务器上保持活动状态：

```bash
screen -S migration          # new session named "migration"
# run ./bin/console commands here; when you want to disconnect without stopping work:
# press Ctrl+A, release, then press d   # detach
screen -ls                   # list sessions
screen -x migration          # reattach to "migration"
```

如果服务器上有`tmux`，您也可以使用该服务器。

### 构建Docker图像

生成`bin/console`使用的[!DNL Docker]映像，其中包含PHP、CLI和依赖项。 在首次运行之前，或在Dockerfile或基本映像更改之后运行它。

```bash
./bin/console build
```

### 启动后备服务

启动该工具的[!DNL Docker Compose]支持服务，例如本地测试数据库，在`.env`中启用时，启动可选的本地服务。 确切的服务取决于您的配置。 在成功构建之后并在shell、迁移或分阶段命令之前运行此命令。

```bash
./bin/console start
```

### 初始化CLI容器

启动一次CLI容器，以便入口点可以针对已装载的项目完成安装，例如根据需要完成[!DNL Composer]安装。 首次在新的环境中运行迁移之前，请运行一次。

```bash
./bin/console shell
exit
```

### 运行迁移

该工具支持两种迁移方法。 选择适合您的用例的库。

#### 单相迁移

源实例上不需要维护模式。 使用单个命令运行完整的迁移管道：

```bash
./bin/console migration
```

该命令按照以下顺序自动运行所有管道步骤（从头到尾）。

1. **配置检查** — 验证环境变量和工具设置。
1. **环境初始化** — 启动[!DNL Docker]服务，打开云隧道（如果适用），并运行单元测试。
1. **集成测试和CDMS初始化** — 运行集成测试并初始化CDMS API连接。
1. **创建迁移** — 向CDMS注册迁移并等待目标架构分析。 迁移ID已保存到`.migration_id`。
1. **功能测试和测试数据生成** — 运行功能测试并在源上生成综合测试数据以进行完整性验证（如果已启用）。
1. **数据提取** — 从源实例提取数据。
1. **加载到目标** — 将提取的数据加载到目标[!DNL Adobe Commerce as a Cloud Service]实例。 源上的暂存视图会被清除，源测试数据会通过REST与负载并行删除。
1. **数据完整性验证** — 触发校验和验证并运行本地API验证测试。 结果将被记录，并且失败不会停止管道。
1. **目标**&#x200B;上的测试数据清理 — 从目标实例中删除合成测试数据。
1. **处理结果** — 生成迁移摘要并可以选择从存储中下载项目。

当不需要维护窗口时（典型情况是端到端练习、开发或沙盒环境，或任何在提取期间源可以保持活动状态的迁移），可使用此选项。

>[!WARNING]
>
>在需要冻结的来源时（例如，在提取期间不得发生新订单或数据更改的任何生产迁移），请勿使用此选项。 请改用分阶段迁移。 请勿将此命令用作分阶段维护工作流中的步骤。

#### 具有维护模式的多阶段迁移

源实例上需要维护模式，以确保提取期间的数据一致性。 迁移将拆分为不同的阶段，您必须按顺序运行这些阶段。

>[!NOTE]
>
>涉及两个不同的CLI。 `./bin/console`命令从迁移工具项目根目录运行。 `bin/magento maintenance:*`命令在源[!DNL Adobe Commerce]应用程序服务器上运行，通过SSH到安装根或通过[!UICONTROL Admin]。 该工具不代表您发出[!DNL Magento]个维护命令。

| 阶段 | 谁运行它 | Source州 |
| --- | --- | --- |
| 1. `migration:before-maintenance` | 工具 | 实时 — 尚未启用维护 |
| &#x200B;2. 启用维护模式 | 手动 | 过渡到冻结 |
| 3. `migration:during-maintenance` | 工具 | 冻结 — 在此阶段不禁用维护 |
| &#x200B;4. 禁用维护模式 | 手动（视情况而定） | 将源实例转换回活动状态 |
| &#x200B;5. `migration:cleanup` （可选） | 工具 | 已上线 — 必须停止维护 |

**阶段1 — 维护之前（源已上线）**

在源实例处于活动状态并接受流量时运行。 必须完全提供REST和GraphQL对源的访问权限。 在此阶段完成之前不要启用维护模式。

返回到服务器根目录并运行：

```bash
./bin/console migration:before-maintenance
```

1. **配置检查** — 验证环境变量和工具设置。
1. **环境初始化** — 启动[!DNL Docker]服务，打开PaaS云隧道（如果适用）并运行单元测试。
1. **集成测试和CDMS初始化** — 运行集成测试并初始化CDMS API连接。
1. **创建迁移** — 向CDMS注册迁移并等待目标架构分析。 迁移ID已保存到`.migration_id`。
1. **功能测试** — 针对实时源运行功能测试。
1. **测试数据生成** — 在源上创建综合测试客户和订单以进行完整性验证（如果已启用）。

**阶段2 — 启用维护模式（手动）**

在源系统上启用维护模式并暂停所有写入或影响数据库的活动，包括计划作业、第三方集成、订单处理和媒体资产同步。

在源Commerce服务器（安装根目录）上，运行：

```bash
bin/magento maintenance:enable
```

**阶段3 — 维护期间（源已冻结）**

在维护模式下使用源实例运行。 在此阶段的整个过程中，源必须保持冻结。 在&#x200B;**阶段3**&#x200B;成功完成之前，请勿禁用维护模式。

```bash
./bin/console migration:during-maintenance
```

1. **云隧道设置** — 对于[!DNL Adobe Commerce on Cloud]源实例，重新打开云隧道并验证数据库连接。 已自动跳过本地实例。
1. **数据提取** — 从冻结的源实例提取数据。
1. **临时视图清理** — 使用直接数据库连接（在维护模式下安全）从源中删除临时视图。
1. **加载到目标** — 将提取的数据加载到目标[!DNL Adobe Commerce as a Cloud Service]实例并等待完成。
1. **数据完整性验证** — 触发CDMS校验和验证并运行本地API验证测试。 结果将被记录，并且失败不会停止管道。
1. **目标**&#x200B;上的测试数据清理 — 从目标实例中删除合成测试数据。
1. **处理结果** — 生成迁移摘要并可以选择从存储中下载项目。

**阶段4 — 禁用维护模式（手动，有条件）**

此阶段将禁用维护模式，并重新启用到源实例的流量。 运行清理阶段之前需要执行此步骤，因为清理通过REST与源进行通信，如果维护模式仍处于活动状态，则清理将失败并显示`HTTP 503`。

在源Commerce服务器上，运行：

```bash
bin/magento maintenance:disable
```

**阶段5 — 清理（可选，源必须处于活动状态）**

通过REST从源实例中删除在&#x200B;**阶段1**&#x200B;中创建的合成测试客户和订单。 此阶段只能在禁用维护模式后运行。

>[!NOTE]
>
>如果`SKIP_TEST_DATA_CREATION=true`在`.env`中设置，则跳过此阶段，因为未创建测试数据。

返回到服务器根目录并运行：

```bash
./bin/console migration:cleanup
```

1. **数据库连接设置** — 对于[!DNL Adobe Commerce on Cloud]源实例，重新打开云隧道。 对于内部部署实例，建立并验证直接数据库连接。
1. **Source REST清理** — 通过REST API从源中删除合成测试客户和订单。

## 恢复或重新运行迁移

迁移工具使用项目根目录中的`.migration_id`文件跟踪进度。 此文件会在新迁移开始时自动创建，并记录当前的迁移标识符。

### 失败后恢复

如果迁移运行失败或中断，请重新运行同一命令以从上一个成功步骤（提取、加载或验证）中恢复，而不是从头开始重新启动。 已完成的步骤会自动跳过。

>[!IMPORTANT]
>
>在恢复`migration:during-maintenance`阶段时，源必须始终处于维护模式。 如果源已退出维护或在运行之间更改了数据，则继续迁移可能会产生不一致的结果。

### 开始新的迁移

要放弃上一次运行并开始全新的迁移，请在开始下一次迁移之前删除`.migration_id`文件：

```bash
rm .migration_id
```

如果`.migration_id`存在并且上一次迁移已经完成，则工具会打印一条消息，说明迁移已经完成，建议您删除该文件。

## 查看日志并调试

所有迁移日志将写入项目根目录中的`logs/`目录，并组织为带时间戳的子目录：

```text
logs/
  2026-03-23_14-30-00/     ← one directory per run
    index.log              ← main pipeline log (start here)
    ...
```

- `index.log`是主管道业务流程日志。 如果某个步骤失败，则会显示使用非零代码退出的脚本以及原因。
- 每个步骤的日志，如`09b_run_load.log`和`11_verify_data_integrity_local.log`，包含每个阶段的详细输出。
