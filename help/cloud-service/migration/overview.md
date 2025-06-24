---
title: 迁移到 [!DNL Adobe Commerce as a Cloud Service]
description: 了解如何迁移到 [!DNL Adobe Commerce as a Cloud Service]。
exl-id: 9065c92a-f6b2-4464-8ec0-5c549bf78104
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目(Adobe管理的SaaS基础架构)。"
role: Architect
source-git-commit: 8b492853442dc64eb9e9592bdf2b695f65d625b8
workflow-type: tm+mt
source-wordcount: '3030'
ht-degree: 0%

---

# 迁移到[!DNL Adobe Commerce as a Cloud Service]

{{accs-early-access}}

[!DNL Adobe Commerce as a Cloud Service]为开发人员提供了从现有Adobe Commerce PaaS实施过渡到新Adobe Commerce as a Cloud Service (SaaS)产品的全面指南。 Adobe Commerce as a Cloud Service代表着向完全托管、无版本SaaS模型的重大转变，提供了增强的性能、可扩展性、简化的操作，以及与更广的Adobe Experience Cloud的更紧密集成。

>[!NOTE]
>
>有关迁移工具的详细信息，请参阅[批量数据迁移工具](./bulk-data.md)。

## 了解这一转变 — 比较PaaS和SaaS

**主要差异**

* 仅[!BADGE PaaS]{type=Informative url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于云项目(Adobe管理的PaaS基础架构)和内部部署项目上的Adobe Commerce 。"} **PaaS（当前）**：商家在Adobe的托管环境中管理应用程序代码、升级、修补和基础架构配置。 [共享责任模型](https://experienceleague.adobe.com/zh-hans/docs/commerce-operations/security-and-compliance/shared-responsibility)，适用于服务(MySQL、Elasticsearch等)。
* [!BADGE 仅限SaaS]{type=Positive url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目(Adobe管理的SaaS基础架构)。"} **SaaS（新增 — [!DNL Adobe Commerce as a Cloud Service]）**： Adobe完全管理核心应用程序、基础架构和更新。 商家专注于通过可扩展性点(API、App Builder、UI SDK)进行自定义。 核心应用程序代码已锁定。

**架构影响**

* **无版本平台**：持续更新意味着核心不再进行主要版本升级。
* **微服务和API优先**：更加依赖于API来实现可扩展性和集成。
* **默认为Headless（可选）**：对分离店面的强大支持(例如，由Edge Delivery Services提供支持的Commerce Storefront)。
* **Edge Delivery Services**：对前端性能和部署的影响。

**新工具和概念**
* Adobe Developer App Builder的[Adobe Developer App Builder](https://developer.adobe.com/app-builder/)和[API Mesh](https://developer.adobe.com/graphql-mesh-gateway)
* [Commerce Optimizer](../../optimizer/overview.md)
* [Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=zh-Hans)
* 使用[Commerce Cloud Manager](../getting-started.md#create-an-instance)进行自助配置

## 迁移路径

[!DNL Adobe Commerce as a Cloud Service]支持多个迁移路径，具体取决于您的时间线、店面和自定义设置。

作为完整迁移的替代方法，[!DNL Adobe Commerce as a Cloud Service]支持使用Commerce Optimizer或增量方法执行分阶段迁移。

* **增量迁移** — 此方法包括分阶段迁移您的数据、自定义项和集成。 这种方法非常适用于具有许多自定义项的大型商家，这些商家希望按照自己的步调将其复杂的自定义项和数据逐步过渡到[!DNL Adobe Commerce as a Cloud Service]。

![增量迁移](../assets/incremental.png){width="600" zoomable="yes"}

* **Commerce Optimizer** — 此方法允许您循环迁移，方法是使用Commerce Optimizer作为过渡阶段，按照自己的步调将复杂的自定义项和数据移动到[!DNL Adobe Commerce as a Cloud Service]。 Commerce Optimizer提供对由目录渠道和策略提供支持的促销服务、由Edge Delivery提供支持的Commerce店面以及由AEM Assets提供支持的产品可视化图表的访问权限。

![迭代迁移](../assets/optimizer.png){width="600" zoomable="yes"}

* **完全迁移** — 此方法包括同时迁移所有数据、自定义项和集成。 这种方法非常适用于那些自定义项很少且想要快速过渡到[!DNL Adobe Commerce as a Cloud Service]的小型商家。

下表概述了不同存储前端和配置的迁移过程：

|                    | LUMA店面 | PWA店面 | 由Edge Delivery提供支持的Commerce店面 | Headless |
|--------------------|----------------------------------------|----------------------------------------|------------------------------------------------------|----------------------------------------|
| 数据迁移 | 必填 | 必填 | 必填 | 必填 |
| 店面 | 迁移到由Edge Delivery提供支持的Commerce Storefront | 迁移到由Edge Delivery提供支持的Commerce Storefront或进行维护 | 无影响 | 无影响 |
| API网格 | 构建新网格 | 构建新网格或重新配置现有网格 | 构建新网格或重新配置现有网格 | 构建新网格或重新配置现有网格 |
| 集成 | 利用集成入门工具包 | 利用集成入门工具包 | 利用集成入门工具包 | 利用集成入门工具包 |
| 自定义 | 移动到App Builder和API Mesh | 移动到App Builder和API Mesh | 移动到App Builder和API Mesh | 移动到App Builder和API Mesh |
| Assets管理 | 使用OOTB时需要迁移 | 使用OOTB时需要迁移 | 使用OOTB时需要迁移 | 使用OOTB时需要迁移 |
| 扩展 | 迁移到App Builder | 迁移到App Builder | 迁移到App Builder | 迁移到App Builder |

如表所示，每次迁移的缓解措施将包括：

* **数据迁移** — 使用提供的[迁移工具](./bulk-data.md)将数据从现有实例迁移到[!DNL Adobe Commerce as a Cloud Service]。
* **店面** — 由Edge Delivery提供支持的现有Commerce店面和headless店面不需要缓解问题，但Luma店面需要迁移到由Edge Delivery提供支持的Commerce店面。 PWA Studio店面可以迁移到由Edge Delivery提供支持的Commerce店面，也可以保持其当前状态。 Adobe将提供加速器以帮助店面迁移。
* **[API网格](https://developer.adobe.com/graphql-mesh-gateway)** — 创建新网格或修改现有网格。 Adobe将提供预配置的网格以帮助完成此过程。
* **集成** — 所有集成都需要利用[集成入门工具包](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/)或[[!DNL Adobe Commerce as a Cloud Service] REST API](https://developer.adobe.com/commerce/webapi/reference/rest/saas/)。
* **自定义项** — 所有自定义项都必须移至App Builder和API网格。
* **Assets管理** — 所有资源管理都需要迁移。 如果您已在使用AEM Assets，则无需迁移。
* **扩展** — 任何进程内扩展都需要重新创建为进程外扩展。 到2025年底，Adobe将提供对我们最受欢迎的扩展的访问，以最大程度地缩短构建时间。

## 迁移阶段

以下阶段描述了迁移到[!DNL Adobe Commerce as a Cloud Service]的必要步骤和注意事项。

### 迁移前评估和规划

此阶段对于最大限度地降低风险、建立明确的迁移路径并在问题出现之前发现问题至关重要。

**发现和审核当前环境**

**代码库分析：**

* 识别所有自定义模块、主题和覆盖。
* 分析核心代码修改，并确定哪些修改需要在迁移过程中进行重构。
* 评估第三方扩展并确定与[!DNL Adobe Commerce as a Cloud Service]的兼容性。 是否有与SaaS兼容的替代方案，或者您是否需要创建自定义API集成或App Builder应用程序？
* 识别任何不会迁移的已弃用代码或功能。

**数据审核：**

* 评估数据库的大小和复杂性。
* 识别未使用的数据或表以进行清理。
* 审查现有数据导入/导出流程。

**集成审核：**

* 列出与Adobe Commerce集成的所有外部系统（ERP、CRM、PIM、支付网关、航运提供商、OMS和任何其他系统）。
* 评估集成方法（API、自定义脚本和其他方法）。
* 评估与[!DNL Adobe Commerce as a Cloud Service]的API优先方法和App Builder的兼容性。

**性能指标评测：**

* 记录当前的Lighthouse分数、页面加载时间和关键绩效指标(KPI)，这为衡量迁移后的改进情况提供了一个基准。

**安全配置审查：**

* 评估任何自定义WAF规则、IP允许列表和任何其他安全配置。

**定义迁移范围和策略：**

* **分阶段迁移与一次性迁移：**&#x200B;评估每种方法的优劣。
* **确定核心业务流程：**&#x200B;优先处理必须首先迁移的功能，例如：
   * 复杂的定价规则
   * 在正式下达或处理订单之前应用的自定义业务规则
   * 复杂的税费计算
   * 地址验证
   * 下达订单后触发的自定义逻辑
* **Headless与整体式店面：**&#x200B;新店面开发或调整现有店面的决策点。
* **集成策略：**&#x200B;确定如何重新规划现有集成(API网格、App Builder、直接API)。
* **数据迁移策略：**&#x200B;确定您打算使用完整历史数据、部分数据还是未迁移的数据进行迁移。

**团队准备和培训：**

* 熟悉[!DNL Adobe Commerce as a Cloud Service]概念、开发工作流和新工具。
* 参加Adobe App Builder、Edge Delivery Services和[!DNL Adobe Commerce as a Cloud Service]部署管道的实践培训。

**环境设置和设置：**

* 使用Commerce Cloud Manager配置您的[!DNL Adobe Commerce as a Cloud Service]沙盒和开发环境。

### 增量迁移阶段

**策略重构和外部化**

此阶段包含迁移的核心，侧重于使代码库适应[!DNL Adobe Commerce as a Cloud Service]云原生范式。 这包括从战略上采用新的Adobe服务和将自定义逻辑移出核心Commerce平台。

#### 1.将“处理中”自定义项和扩展迁移到App Builder

这是实现“锁定核心”和面向未来的解决方案的关键阶段，是[!DNL Adobe Commerce as a Cloud Service]架构理念的核心。

* **将复杂逻辑外部化到App Builder**：分析PaaS代码库中的现有自定义模块和第三方扩展。 对于复杂的业务逻辑、定制集成或微服务，它们不需要直接、在进程中操作核心Commerce数据模型，请在Adobe Developer App Builder中将它们重构并重新平台为无服务器应用程序。
* **利用API Mesh**：对于需要来自多个后端系统(例如，您的PaaS Commerce后端、ERP、CRM和自定义App Builder微服务)的数据的情况，请在App Builder中实施API Mesh层。 这会将不同的API整合到单个高性能的GraphQL端点中，供您的新店面或其他服务使用，从而简化复杂的数据提取。
* **事件驱动型架构**：利用Adobe I/O Events根据PaaS实例中发生的事件（例如，产品更新、客户注册、订单状态更改）或其他连接系统中发生的事件，触发App Builder操作。 这促进了异步通信，降低了紧密耦合，并增强了系统恢复能力。

**好处**：此步骤可显着减少与深度嵌入的自定义项相关的技术债务，显着加快将Commerce实例过渡到[!DNL Adobe Commerce as a Cloud Service]的速度，增强自定义逻辑的可扩展性和独立部署能力，并加快扩展的开发周期。

#### 2.采用基于SaaS的Adobe Commerce促销服务并集成目录数据

这是一个关键的初始集成点，它有两个关于目录数据管理的选项：

>[!BEGINTABS]

>[!TAB 选项1 — 现有目录SaaS服务]

**利用与PaaS后端集成的现有目录SaaS服务**

此选项用作过渡步骤，以现有集成为基础，在该集成中，PaaS后端使用[目录服务](../../catalog-service/guide-overview.md)、[实时搜索](../../live-search/overview.md)和[产品推荐](../../product-recommendations/overview.md)中的数据填充Adobe Commerce SaaS服务的现有实例。

* **目录数据同步**：确保您的Adobe Commerce PaaS实例继续将产品和目录数据同步到您现有的Adobe Commerce目录SaaS服务。 这通常依赖于PaaS实例中已建立的连接器或模块。 目录SaaS服务仍然是搜索和促销功能的权威来源，其数据来自PaaS后端。
* 用于优化的&#x200B;**API网格**：虽然Headless店面(在Edge Delivery Services上)和其他服务可以直接使用目录SaaS服务中的数据，但Adobe强烈建议使用API网格(在App Builder内)。 API网格可以将目录SaaS服务中的API与PaaS后端中的其他必要API（例如，来自事务性数据库的实时清单检查或未完全复制到目录SaaS服务的自定义产品属性）统一到单个高性能GraphQL端点中。 这还可以实现集中式缓存、身份验证和响应转换。
* **集成实时搜索和产品推荐**：将实时搜索和产品推荐SaaS服务配置为直接从现有Adobe Commerce目录SaaS服务[摄取目录数据](https://experienceleague.adobe.com/zh-hans/docs/commerce/live-search/install#configure-the-data)，而您的目录SaaS服务又由PaaS后端填充。

**优势**：通过利用现有的可操作目录SaaS服务及其与PaaS后端的集成管道，这可以更快地通向Headless店面和高级SaaS促销功能。 但是，它保留了对主目录数据源的PaaS后端的依赖关系，并且不提供新的可组合目录数据模型中固有的多源聚合功能。 此选项是实现更完整可组合架构的有效基础。

>[!TAB 选项2 — 可组合的目录数据模型]

**采用新的可组合目录数据模型(CCDM)**

这是经得起未来考验的战略性方法来利用Adobe Commerce Optimizer。 CCDM提供了灵活、可扩展且统一的目录服务，专为多源数据聚合和动态促销而设计。

* **数据摄取和统一**
   * 首先，将现有Adobe Commerce PaaS实例（和/或其他PIM/ERP系统）中的产品和目录数据引入新的可组合目录数据模型(CCDM)。
   * 将现有的产品属性映射到CCDM的灵活架构。 优先考虑关键产品数据以进行初始摄取。
   * 为连续同步建立可靠的数据管道。 这可能包括：
      * **事件驱动**(通过App Builder)：利用PaaS实例中的Adobe I/O Events触发公开可用或自定义Adobe App Builder应用程序。 这些应用程序通过其API转换数据更改（创建、更新和删除）并将其推送到CCDM。
      * **批量摄取**：对于大型初始加载或定期批量更新，请使用安全文件传输（例如CSV或JSON）到临时区域，由Adobe Experience Platform (AEP)摄取服务处理到CCDM。
      * **直接API集成**(与App Builder编排)：对于更复杂的场景，App Builder可以充当编排层，对您的PaaS后端进行直接API调用，转换数据，并将其推送到CCDM。
* **目录视图和策略定义**：在CCDM中配置目录视图（用于唯一目录呈现的逻辑分组，例如商店视图、区域和B2B/B2C区段）并定义策略（用于产品呈现、筛选和促销的规则集）。 这样可动态控制每个渠道的产品分类和显示逻辑。
* **集成实时搜索和产品推荐**：一旦目录数据出现在CCDM中，就集成Adobe基于SaaS的实时搜索和产品推荐服务。 这些模型利用Adobe Sensei AI和机器学习模型实现卓越的搜索相关性和个性化推荐，直接从CCDM使用数据。

**优势**：通过将目录管理和发现抽象到CCDM和关联的SaaS服务中，您可以提高性能，获得AI驱动的促销功能，显着减轻旧式后端读取操作的负载，并实现对漏斗顶部体验的强大“剥离”。

>[!ENDTABS]

#### 3.在Edge Delivery Services上建立您的店面

随着建立促销数据管道和将自定义项外部化，焦点将转移到构建高性能的前端。

* **初始设置**：使用Edge Delivery Services的Adobe Commerce店面模板设置项目。 这为基于现代Web技术构建的Headless前端提供了基础。
* **连接到目录服务和API Mesh**：您的Commerce店面将主要通过GraphQL API使用数据：
   * **选项1**：从现有的目录SaaS服务（通过API Mesh）获取产品信息和促销规则。
   * **选项2**：从CCDM获取产品信息和促销规则。
   * 从API Mesh获取旧版后端（PaaS实例）或自定义App Builder服务中的任何编排数据（例如，显示实时库存、自定义产品属性和忠诚度点数）。
* **内容迁移(AEM服务)**：将您现有的静态内容（例如，“关于我们”页面、博客文章和营销横幅）迁移到支持Commerce店面的AEM服务。 利用AEM的内容创作功能并确保针对Edge Delivery Services优化资产。
* **开发核心UI组件**：使用Edge Delivery Services插件组件和自定义React/Vue组件为产品详细信息页面(PDP)、产品列表页面(PLP)和常规内容页面构建关键用户界面组件。 确定核心商务流的优先级。
* **与现有购物车/结帐集成**：最初，Edge Delivery Services店面将协调您向现有Adobe Commerce PaaS（或其他第三方平台）的切换，以进行购物车管理和结帐。 这通常涉及：
   * **重定向**：将用户重定向到旧版平台的本机购物车和结帐URL，并传递必要的会话和购物车标识符。
   * **直接API交互**(使用App Builder编排)：在Edge Delivery Services中构建直接与PaaS后端的购物车和结帐API交互的自定义购物车和结帐UI组件。 这通常涉及将App Builder作为前端后端(BFF)来编排对多个后端服务（例如，PaaS cart、支付网关和配送计算器）的调用。

**优势**：提供超快、SEO优化和高度灵活的店面体验。 此阶段直接有助于提供卓越的客户体验，并为未来前端创新奠定基础。

#### 4.数据迁移（分阶段过程）

数据迁移是一个关键的、多方面的过程，它与重构和店面开发同时运行，从而确保数据一致性和完整性。

* **清理和优化现有数据**：在任何大规模迁移之前，对现有PaaS数据库执行全面的数据清理、重复数据消除和验证。 此主动步骤对于最大限度地减少旧数据问题的传输并确保新环境中的数据质量至关重要。

**批量数据迁移**

批量数据迁移包括从Adobe Commerce PaaS实例中获取完整数据转储，转换整个数据集，并将其导入Adobe Commerce as a Cloud Service中，所有这些操作都可以同时完成。 此方法通常用于初始数据群体。

* **工具可用性**：将在2025年7月中旬应请求提供专门的[批量数据迁移工具](./bulk-data.md)，以供客户用于第一方Commerce批量数据迁移。 如果客户在批量数据迁移之前需要帮助，Adobe可以代表他们根据请求促进数据传输。

* **进程**：
   * **完整数据导出**：从Adobe Commerce PaaS实例中提取完整的数据集（例如，产品、类别、客户帐户、历史订单数据、静态块和页面内容）。
   * **数据转换**：应用必要的转换以使提取的数据符合新Adobe Commerce as a Cloud Service组件的架构要求，包括可组合目录数据模型(CCDM)（如果采用）以及任何其他相关Adobe服务或数据库。 这可能涉及自定义脚本或专门的数据映射工具。
   * **初始导入**：将转换后的完整数据集导入Adobe Commerce as a Cloud Service的相应组件中。 对于产品和类别数据，这将填充所选的目录服务（CCDM或现有的目录SaaS）。 对于客户和订单数据，这将填充事务型后端或关联的服务。
   * **验证**：严格验证导入的数据，以确保所有新系统的完整性、准确性和一致性。

**迭代数据迁移**

迭代数据迁移侧重于将增量更改和删除从源PaaS实例同步到新的Cloud Service组件，确保数据在转换之前和之后保持新鲜。

* **工具可用性**：专门为迭代数据迁移设计的工具将在2025年下半年推出。

* **进程**：
   * **增量标识**：建立机制以标识自上次同步以来PaaS环境中关键数据集中的更改（创建、更新和删除）。 这可能涉及更改数据捕获(CDC)、时间戳比较或基于事件的触发器。
   * **连续同步**：为从PaaS环境到新Cloud Service组件（例如，CCDM和事务性后端）的连续、增量数据同步实施可靠的机制。 这对于保持数据新鲜度以及在转换期间最大程度地减少停机时间至关重要。
   * **利用事件**：尽可能利用Adobe I/O Events触发App Builder操作，以便从您的PaaS实例实时或近乎实时地更新新服务。 例如，PaaS中的产品更新可能会触发一个事件，该事件会更新CCDM中的相应条目。
   * **API驱动更新**：对于非事件驱动的数据，使用计划的API调用(通过App Builder或其他集成平台)从PaaS中提取更改并将它们推送到新系统。
   * **错误处理和监控**：对所有迭代数据管道实施可靠的错误处理、日志记录和监控，以确保在整个过程中保持数据完整性。

### 迁移后和日常操作

**DNS直接转换并上线：**

* 仔细规划DNS切换，最大限度地减少停机时间。
* 启动后立即监控站点运行状况和性能。

**启动后操作：**

**正在停用PaaS环境：**

* 在验证期过后，安全地存档或删除旧的PaaS实例和数据。

**正在进行的开发工作流：**

* 接受[!DNL Adobe Commerce as a Cloud Service]的无版本特性，它具有连续的小部署而不是大型升级。
* 利用Cloud Manager管理环境和部署。
* 利用App Builder扩展功能而不影响核心。

**监控、性能和安全性：**

* 持续监控站点性能、错误和安全日志。
* 利用Adobe的内置安全功能并遵循最佳实践。

**培训和文档：**

* 针对[!DNL Adobe Commerce as a Cloud Service]平台和工作流程培训新开发人员和业务用户。
* 维护自定义集成和流程的最新内部文档。
