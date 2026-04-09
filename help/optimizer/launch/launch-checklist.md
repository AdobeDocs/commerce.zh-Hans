---
title: 启动项核对清单
description: 了解如何验证 [!DNL Adobe Commerce Optimizer] 生产环境的配置、店面、SEO、CDN、集成、安全性、分析和测试。
solution: Commerce
feature: Integration, Storefront, Search, Catalog Management, Personalization
feature-set: Commerce
role: Admin, Developer
level: Intermediate
topic: Administration
recommendations: noCatalog
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和 [!DNL Adobe Commerce Optimizer] 项目（Adobe管理的SaaS基础架构）。"
source-git-commit: 37b8b8a334ca11daacfd3da03b0441e77329e2e1
workflow-type: tm+mt
source-wordcount: '1940'
ht-degree: 0%

---


# 启动项核对清单

使用此核对清单验证您的生产[!DNL Adobe Commerce Optimizer]项目是否已配置、测试并准备好启动。 与您的团队一起处理每个部分，并在您自己的项目计划或跟踪器中跟踪完成情况。 有关下面引用的产品功能和UI区域，请参阅[[!DNL Adobe Commerce Optimizer] 文档](../overview.md)。

## 用例和架构 {#use-case}

当您交付的B2C体验将[!DNL Adobe Commerce Optimizer]和Edge Delivery Services (EDS)与Cloud实例上的现有Adobe Commerce结合时，请使用此核对清单。

您的解决方案通常包括以下组件：

- **Cloud**—Adobe Commerce on Cloud管理目录数据、客户、资源和采购流程（结账、订单管理、配送等）。
- **优化器**—[!DNL Adobe Commerce Optimizer]提供促销体验。
- **Storefront**—Edge Delivery Services上的Adobe Commerce Storefront提供UI。
- **第三方服务** — 付款、送货和税务提供商。
- **App Builder** — 可扩展性。
- **API网格** — 请求路由。

## 在云中验证Adobe Commerce {#verify-cloud}

确认您的Adobe Commerce on Cloud环境已准备好进行生产。

▢云实例为[已设置](https://experienceleague.adobe.com/zh-hans/docs/commerce-on-cloud/start/new-project)。
▢从实例中删除测试和虚拟数据。
已在实例上加载▢生产数据。
▢您知道[GraphQL终结点](https://developer.adobe.com/commerce/webapi/graphql/)。
▢实例符合[准备启动](https://experienceleague.adobe.com/zh-hans/docs/commerce-on-cloud/user-guide/launch/checklist)要求。

## 验证Commerce Optimizer实例 {#verify-optimizer}

确认您的[!DNL Adobe Commerce Optimizer]生产实例已正确设置。

▢生产实例处于活动状态。 请参阅[入门](../get-started.md)以了解如何配置它。
▢实例位于正确的区域。
▢环境类型为“生产”。
▢您知道组织ID、客户端ID、摄取URL和Commerce Optimizer URL。 请参阅[开始使用](../get-started.md)。
▢配置的限制和边界与您的Adobe客户技术顾问(CTA)确认的值相匹配。
▢测试工件和虚拟数据已从实例中删除。

## 验证店面站点 {#verify-storefront-site}

确认您的Edge Delivery Services店面网站存在并且访问受限。

▢店面站点存在。 请参阅[创建店面](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/?lang=zh-Hans)。
▢您知道站点名称。
▢只有授权人员才有[权限发布](https://tools.aem.live/tools/user-admin/index.html)。
▢只有授权人员才有[创作权限](https://docs.da.live/administrators/guides/permissions)。

## 验证Cloud和Optimizer集成 {#cloud-optimizer-integration}

确认Adobe Commerce on Cloud和[!DNL Adobe Commerce Optimizer]正确交换数据。

### 在Adobe Commerce上

在云项目中完成这些检查。

▢ Commerce Optimizer连接器已[安装并配置](../../aco-connector/get-started.md)。
▢ `aco:conf:show` CLI命令确认与Commerce Optimizer生产实例的连接。 组织ID、客户端ID、摄取URL和Commerce Optimizer URL与生产环境相匹配。
▢导出配置[中的](../../aco-connector/get-started.md)同步作用域符合您的要求。
▢ [数据馈送同步状态](../../aco-connector/get-started.md)确认从云实例导出数据。

### 在Commerce Optimizer中

在[!DNL Adobe Commerce Optimizer] UI中完成这些检查。

▢ [数据同步仪表板](../setup/data-sync.md)显示接收的数据。 此时将显示“目录服务”、“产品发现”和“推荐”的产品、价格和属性。
▢ [价格手册](../setup/pricebooks.md)是从云上的客户组自动创建的。
▢ [目录视图](../setup/catalog-view.md)存在并且您知道它们的ID。
▢ [策略](../setup/policies.md)存在并且您知道它们的ID。
已配置▢ [Facet](../merchandising/facets/overview.md)。
已配置▢ [同义词](../merchandising/synonyms/overview.md)。
已配置▢ [促销规则](../merchandising/rules/overview.md)。
使用这些功能时，▢ [价格彩块化和搜索语言](../settings.md)符合您的要求。
▢ [产品推荐](../merchandising/recommendations/create.md)存在，并在预览中按预期运行。
▢ [搜索性能数据](../manage-results/search-performance.md)出现在&#x200B;*管理员*中。
▢ [推荐性能数据](../manage-results/recommendation-performance.md)显示在&#x200B;*管理员*&#x200B;中。

## 验证店面和云集成 {#storefront-cloud-integration}

确认店面是否从正确的Adobe Commerce GraphQL端点读取。

### 在Adobe Commerce上

▢ Storefront兼容包是[安装的](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility/install/?lang=zh-Hans)。

### 在店面

▢店面`commerce-core-endpoint`设置指向您的[Cloud GraphQL终结点](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/?lang=zh-Hans)。
▢如果您使用API Mesh作为Cloud GraphQL的代理，`commerce-core-endpoint`将指向API Mesh端点而不是Cloud GraphQL端点。

## 验证storefront和Optimizer集成 {#storefront-optimizer-integration}

确认店面配置中的Commerce Optimizer设置。

▢您的店面使用正确的[Commerce Optimizer设置](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/?lang=zh-Hans)。
▢ `adobe-commerce-optimizer`是`true`。
▢ `commerce-endpoint`指向生产Commerce Optimizer GraphQL端点，或您使用API网格时的API网格端点。
▢ `headers.cs.AC-view-ID`包含来自生产Commerce Optimizer实例的目录视图ID。

## 验证云上的第三方服务 {#third-party-services}

确认在您的主机商务系统上运行的集成（不在[!DNL Adobe Commerce Optimizer]中）。

▢ **支付：**&#x200B;支付网关已上线并经过测试（Stripe、PayPal、Adyen等）。
▢ **送货：**&#x200B;送货API连接工作（UPS、FedEx等）。
已连接并测试▢ **配送：**&#x200B;履行平台（例如，ShipStation）。
▢ **税：**&#x200B;已验证税计算集成（Avalara、TaxJar等）。
▢ **税费：**&#x200B;会计软件同步工作（QuickBooks等）。
▢ **清单：** PIM、ERP或清单管理集成已测试并同步。
▢ **架构：**&#x200B;主机商务系统处理付款、运费、税收和库存（非[!DNL Adobe Commerce Optimizer]）。
▢ **架构：** API Mesh和App Builder在主机商务系统与[!DNL Adobe Commerce Optimizer]之间保持同步。
▢ **电子邮件：**&#x200B;事务性电子邮件投放的工作方式（订单确认、送货等）。
▢ **电子邮件：**&#x200B;电子邮件模板与您的品牌匹配并使用正确的链接。

## 验证App Builder和API网格 {#app-builder-mesh}

确认生产的可扩展性配置。

### App Builder

▢生产工作区包括所有必需的配置和服务。
▢生产应用程序通过了各种生成方案的测试。
已根据▢Adobe Developer App Builder产品描述[和](https://helpx.adobe.com/cn/legal/product-descriptions/adobe-developer-app-builder.html){target="_blank"}App Builder系统设置和限制[审核并确认](https://developer.adobe.com/app-builder/docs/guides/runtime_guides/system-settings){target="_blank"}产品限制和范围。
▢生产应用程序使用App Builder生产端点。
▢自定义&#x200B;*Admin*&#x200B;面板扩展已部署到生产工作区。

### API网格

▢配置和源已准备就绪，可供生产。

### 活动

已配置▢个Adobe I/O Events并验证订阅。

## 最终确定店面体验 {#finalize-storefront}

发布之前的波兰内容、SEO、性能、安全性和CDN行为。

### 内容和创作

确认创作工作流和店面组件。

▢ [AEM/EDS上线核对清单](https://www.aem.live/docs/go-live-checklist)审核已完成。
▢创作源是基于文档的编辑器或通用编辑器（已配置）。
使用预览→发布周期发布▢内容。
▢域上的`.aem.live`内容和设计QA已完成。
▢ Favicon已正确配置并由站点提供服务。
▢ da.live和产品可视化使用[已配置](https://docs.da.live/administrators/guides/permissions)专用凭据。
▢个下拉列表（购物车、结帐、PDP、PLP、身份验证、帐户）已自定义[并已测试](../storefront.md)。
▢店面品牌反映了CSS设计令牌、排版和颜色。

### SEO和索引

确认元数据、URL和抓取行为。

▢关键页（尤其是PDP和PLP）存在文档标题元数据。 请参阅[Adobe Commerce店面](https://experienceleague.adobe.com/developer/commerce/storefront/setup/seo/metadata/?lang=zh-Hans){target="_blank"}文档中的&#x200B;_SEO元数据_。
▢ PDP包括[元数据和结构化数据](https://experienceleague.adobe.com/developer/commerce/storefront/setup/seo/metadata/?lang=zh-Hans){target="_blank"}（例如，JSON-LD）。
▢产品URL格式一致（例如，`domain/product-name`）。
▢虚URL重定向到规范URL。
▢项目包括`robots.txt`，它允许在适当时进行索引、引用Sitemap并阻止您不希望进行索引的路径（例如，`/drafts`）。
▢ [重定向](https://www.aem.live/docs/redirects)文件涵盖迁移中的URL更改（例如，在删除`.html`之后）。
▢ Sitemap存在并根据需要提交到Google搜索控制台。
▢规范URL返回`2xx`状态（不是`3xx`或`4xx`）。
▢多语言站点在站点地图中包含`hreflang`标记。
▢ Google Search Console覆盖范围报告是最新的。

### 预渲染

确认启用服务器端渲染的位置。

为关键页面启用了▢预呈现。 请参阅[AEM店面](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-prerender/?lang=zh-Hans){target="_blank"}文档中的&#x200B;_Adobe Commerce的预呈现_。
▢个URL使用小写，因此预渲染不会断开链接。
▢ HTML源包含确认预呈现工作的元数据和正文内容。
▢区域设置显示正确的已翻译页面（如果适用）。
▢其他HTML标记是[根据需要配置的](https://www.aem.live/docs/redirects)。

### 性能和监控

确认性能基线和分析布线。

▢您的店面遵循[Adobe Commerce店面](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/performance/?lang=zh-Hans){target="_blank"}文档中的&#x200B;_性能最佳实践_。
▢（可选）已配置Google Analytics和Google Tag Manager。
▢ [Storefront事件](https://github.com/adobe/commerce-events/tree/main/examples/events/snowplow-debugger)实现有效，并且数据显示在Adobe Commerce [!DNL Live Search]管理员[!DNL Product Recommendations]的&#x200B;*和*仪表板中。
▢ `environment`Commerce配置[中的](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/?lang=zh-Hans){target="_blank"}分析参数在开发期间为`"Testing"`，在上线时为`"Production"`。 请参阅[Analytics检测](https://experienceleague.adobe.com/developer/commerce/storefront/setup/analytics/instrumentation/?lang=zh-Hans){target="_blank"}。
根据此主题中的指导，▢个Lighthouse分数达到了您的目标（例如，关键页面上的`100`）。

### 安全性和访问权限

确认权限和密钥。

▢为DA内容和EDS站点配置了适当的权限。 查看[DA.live权限](https://da.live/docs/administration/permissions)和创作身份验证设置[&#128279;](https://www.aem.live/docs/authentication-setup-authoring)。
▢已配置产品可视化集成。 请参阅[AEM Cloud Service访问概述](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/cloud-service/accessing/overview#)。
电子邮件模板中的▢密码重置链接与您的Edge Delivery Services设置相匹配。 查看店面常见问题解答：[如果迁移到Edge Delivery Services或Helix后我的电子邮件模板链接损坏，我应该怎么做？](https://experienceleague.adobe.com/developer/commerce/storefront/troubleshooting/faq/?lang=zh-Hans#what-should-i-do-if-my-email-template-links-are-broken-after-migrating-to-edge-delivery-services-or-helix){target="_blank"}。
适用于集成和付款提供商的▢生产密钥已准备就绪。
▢域已列入允许列表，后端Webhook可正常工作。

### CDN和缓存

确认CDN、DNS和缓存行为。

▢ CDN配置使用Sidekick扩展和脚本（例如，Sitemap生成和图像导入程序）的GraphQL生产端点(`yourproject.com/graphql`)。
▢当您使用Adobe Commerce Fastly时，CDN清除令牌可用，[站点配置](https://tools.aem.live/tools/cdn-setup/index.html)包括`authToken`和`serviceId`。
▢ [CDN配置](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/content-delivery-network/?lang=zh-Hans){target="_blank"}验证缓存和无效。
▢对于[多存储设置](https://experienceleague.adobe.com/developer/commerce/storefront/setup/seo/indexing/?lang=zh-Hans#multi-store-setups){target="_blank"}，目录服务和[!DNL Live Search]请求包含特定于存储的缓存终结器（例如，查询参数或CDN规则）。
▢推送失效工作以端到端方式进行（发布更改，然后在生产域上验证）。
在直接转换之前，▢ DNS TTL足够低。
所有域和主机名的▢个DNS A和CNAME记录均正确。
▢已为生产域配置并验证SSL/TLS证书。
▢ `www`和Apex重定向行为正确。

## 安全性和合规性 {#security-compliance}

确认安全状态和合规性任务。

▢ **SSL：**&#x200B;已安装受信任的SSL/TLS证书。
▢ **SSL：** HTTPS已在站点范围内强制执行。
▢ **访问：**&#x200B;默认&#x200B;*管理员*&#x200B;密码已更改并且已设置强密码策略。 查看[!DNL Adobe Commerce Optimizer] [用户和身份管理](../user-management.md)。
▢ **访问：** *管理员* URL不是默认URL。
▢ **访问：**&#x200B;已为所有&#x200B;*管理员*用户启用双重身份验证。
▢ **访问：**&#x200B;没有非活动或未使用的管理员用户与项目相关联。
▢ **防火墙：** Web应用程序防火墙(WAF)已配置并验证。
▢ **PCI：**&#x200B;生产（PCI范围）上的安全渗透测试已完成。
▢ **扫描：** Adobe安全扫描工具已注册，初始扫描已完成。
▢ **访问：** CORS仅允许批准的源。
▢ **合规性：** [的](../shared-responsibility.md)责任分担模型[!DNL Adobe Commerce Optimizer]是最新的，并清楚地定义了Adobe与客户责任的对比。
▢ **合规性：**&#x200B;已验证隐私政策、Cookie同意以及GDPR或CCPA要求。

## 分析和监控 {#analytics-monitoring}

确认度量和基线。

▢ **RUM：**&#x200B;实际用户监控(RUM)已检测前后比较。
▢ **Analytics：** Adobe Experience Platform数据收集已配置（如果适用）。
▢ **Analytics：**&#x200B;已验证MarTech标记是否在生产主机名上触发。
▢ **分析：**&#x200B;已记录基线分析；预计在启动后会出现波动（页面查看次数、跳出率等）。
▢ **事件：**&#x200B;转化跟踪工作端对端进行（添加到购物车→结帐→确认）。

## 测试 {#testing}

在启动之前和之后确认质量。

▢ **功能：**&#x200B;核心流工作端对端：浏览→搜索→筛选器→添加到购物车→结帐→帐户创建。
▢ **功能：**&#x200B;付款网关接受真实交易和测试交易。
▢ **功能：**&#x200B;订单投放、确认电子邮件和订单跟踪工作。
▢ **功能：**&#x200B;配送选项和税额计算是准确的。
▢ **功能：**&#x200B;优惠券、折扣和忠诚度计划按预期运行。
▢ **UAT：**&#x200B;用户验收测试已在暂存和生产环境中完成。
▢ **性能：**&#x200B;负载和压力测试已完成，并且Adobe CTA或CSE具有结果。
▢ **性能：**&#x200B;桌面和移动设备上的页面加载时间少于三秒。
▢ **性能：** Lighthouse分数在关键页面上达到目标（例如，通过PageSpeed Insights）。
已优化▢ **性能：**&#x200B;映像、脚本和资产。
▢ **兼容性：** Chrome、Firefox、Safari和Edge按预期运行。
▢ **兼容性：**&#x200B;响应布局适用于移动设备、平板电脑和桌面。
▢ **兼容性：**&#x200B;性能在3G、4G和Wi-Fi上可接受。
▢ **辅助功能：**&#x200B;辅助功能审核已完成（WCAG、屏幕阅读器、键盘导航）。
▢ **功能：**&#x200B;已制定启动后404监视计划。
▢ **UAT：**&#x200B;存在回滚计划，如果发生启动问题，则会通过测试。

## 启动日期和启动后 {#launch-post-launch}

确认通信、支持和后续任务。

▢ **启动协作：** Adobe已确定启动日期；已通过电子邮件通知CTA。
▢ **支持：**&#x200B;已记录P1热线号码：美国(+1) 800-497-0335，然后按6以访问Commerce。
▢ **支持：**&#x200B;您的团队已接受培训，可在调用P1热线之前&#x200B;**打开支持票证**。
▢ **启动后：**&#x200B;验证生产域上的Lighthouse分数。
▢ **启动后：**&#x200B;监视Google搜索控制台以编制索引并抓取错误。
▢ **启动后：**&#x200B;监视404报告，并为高流量旧版URL添加重定向。
▢ **发布后：**&#x200B;确认MarTech和分析生产数据。
▢ **启动后：**&#x200B;请让您的CTA、CSE或AM启用高SLA监控。
▢灾难恢复计划存在并通过测试。
▢已制定流程来跟踪和升级样板和扩展包到当前版本。
