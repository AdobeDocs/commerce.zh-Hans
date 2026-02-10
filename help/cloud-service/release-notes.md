---
title: '[!DNL Adobe Commerce as a Cloud Service]发行说明'
description: 了解 [!DNL Adobe Commerce as a Cloud Service]中的最新功能和改进。
feature-set: Commerce
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Developer, User, Leader
level: Beginner
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目(Adobe管理的SaaS基础架构)。"
exl-id: cf06dec6-8d6b-413e-9977-df88373c188e
source-git-commit: 49762cfcf0e4086ec21815edcfefc0c3971e510f
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 0%

---

# 发行说明

以下发行说明包含[!DNL Adobe Commerce as a Cloud Service]的更新。

>[!NOTE]
>
>如果您正在本地使用Adobe Commerce或在云基础架构上使用Adobe Commerce，请参阅[Adobe Commerce发行说明](https://experienceleague.adobe.com/en/docs/commerce-operations/release/notes/overview)。

## 2026年2月 {#latest}

<!-- [!BADGE Sandbox]{type=Caution tooltip="The items listed are currently only available in Sandbox environments. Adobe makes new releases available in Sandbox environments first to provide time to test upcoming changes before the release is available on Production environments."} -->

[!BADGE 生产]{type=Neutral tooltip="列出的项目当前在生产环境中可用。"}

以下项目已于2026年2月10日发布到[!DNL Adobe Commerce as a Cloud Service]的生产环境。

>[!BEGINSHADEBOX]

### 自定义配送方式并查看管理员报表

对[!DNL Commerce Admin]进行了以下增强：

* 增强了进程外[送货webhook负载](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/shipping-use-cases/#payload)以包含送货地址自定义属性。 这项更改使商家能够实施自定义配送方式。<!-- ACCS-235 -->

* 已添加对管理员报告的访问权限，这些报告包括[客户](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/customer-reports)、[营销](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/marketing-reports)、[产品](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/product-reports)和[销售](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/sales-reports)的报告。<!-- CCSAAS-3085 -->

>[!NOTE]
>
>[!DNL Adobe Commerce as a Cloud Service]中不可用的报告仅标记为PaaS （[!BADGE 仅PaaS &#x200B;]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于云项目(Adobe管理的PaaS基础架构)和内部部署项目上的Adobe Commerce 。"}）。

### 通过REST API捕获自定义发票金额

发票API现在支持使用扩展属性的[自定义捕获金额](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#custom-capture-amounts)。<!-- ACCS-186, ACCS-197, ACCS-143 -->

>[!NOTE]
>
>由于法律限制，自定义捕获金额仅在北美(NA)地区和允许付款超额捕获的其他地区可用。

### 增强功能和错误修复

此版本中包含以下选定的增强功能、优化和错误修复：

* 修复了优惠券网格筛选条件，以显示通过API或通过导入创建的所有自定义优惠券。<!-- CCSAAS-4509 -->

* 修复了[!DNL Storefront Compatibility B2B Package]中的一个问题，即使`setNegotiableQuoteShippingAddress`设置为`save_in_address_book`，`true`突变也不会将手动输入的地址保存到客户的通讯簿中。<!-- LYNX-1031 -->

<!-- The above change will also be covered by the B2B changelog published on February 13, 2026. -->

* 解决了由于与资产角色相关的自定义属性中的[!DNL Edge Delivery Services]值损坏而导致产品图像无法在`no_selection`中正确显示的问题。<!-- ACAP-1206 -->

* 解决了阻止名字或姓氏值为空的联合用户帐户访问Commerce管理员的问题。<!-- ACCS-200 -->

* 通过自动提供特定于区域的IMS客户端ID，简化了资产选择器配置。 商家无需再提交支持票证即可配置资产选择器，以将产品类别图像与资产进行映射。 系统现在会根据Commerce地区自动使用专用的IMS客户端ID。<!-- ACCS-175 -->

* 各种性能和优化改进。<!-- CCSAAS-4485, CCSAAS-4497, ACCS-196 -->

{{accs-release}}

>[!ENDSHADEBOX]

## 2026年1月

[!BADGE 生产]{type=Neutral tooltip="列出的项目当前在生产环境中可用。"}

以下项目已于2026年1月20日发布到[!DNL Adobe Commerce as a Cloud Service]的生产环境。

>[!BEGINSHADEBOX]

### B2B外接程序

对B2B放置组件进行了以下更改：

* [!DNL Commerce Storefront on Edge Delivery Services]现在包含[B2B放置组件](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/)。 以下B2B下拉列表现已可用：

   * **[公司管理](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/company-management/)** — 启用Adobe Commerce店面的公司配置文件管理和基于角色的权限。
   * **[公司切换器](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/company-switcher/)** — 为用户提供UI组件，以便在其关联的多个公司之间进行切换。
   * **[采购订单](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/purchase-order/)** — 管理B2B交易的采购订单工作流、审批规则和采购订单历史记录。
   * **[报价管理](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/quote-management/)** — 为具有报价请求、洽谈和批准工作流的B2B客户启用可协商报价。
   * **[申购单列表](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/requisition-list/)** — 提供用于创建和管理重复购买和批量订购的申购单列表的工具。

* 发布了B2B店面兼容包。 此包增强了[!DNL Adobe Commerce] B2B GraphQL架构，以帮助改进B2B系统上的开发。

<!-- 
* [!DNL Commerce Storefront on Edge Delivery Services] now includes [B2B drop-in components](http://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/). For a complete list of available B2B drop-in blocks, refer to the [storefront documentation](http://experienceleague.adobe.com/developer/commerce/storefront/merchants/b2b-commerce-blocks/).

* Released the [B2B Storefront Compatibility Package](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility-b2b/). This package enhances the [!DNL Adobe Commerce] B2B GraphQL schema to help improve development on B2B systems. -->

### 指向外部配送跟踪器的可点击链接

通过[启用自定义跟踪URL](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/delivery/shipping-settings#shipment-tracking-urls)，将购物者电子邮件中包含的装运跟踪编号从纯文本转换为可点击链接。 USPS、UPS、FedEx和DHL支持此功能。<!-- See PR #716 in commerce-admin -->

### Google reCAPTCHA企业支持

[!DNL Adobe Commerce as a Cloud Service]店面现在支持[reCAPTCHA Enterprise](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/captcha/security-google-recaptcha-enterprise)。 此功能通过使用自适应风险分析和机器学习准确地区分人类用户和自动化机器人，提供高级机器人保护。 它增强了网站安全性，防止了欺诈性活动，并减少了垃圾邮件和滥用，以保持可信的购物体验。<!-- CCSAAS-4242 -->

### 特定于实例的管理员访问权限

您现在可以[将用户访问权限](./user-management.md#add-users)分配给Admin Console中的各个[!DNL Adobe Commerce as a Cloud Service]实例。<!-- CCSAAS-4337 --><!-- See PR #332 -->

### 可观测性

通过使用[!DNL App Builder]，您可以使用[!DNL Adobe Commerce as a Cloud Service]OpenTelemetry可观察性[更深入地了解](https://developer.adobe.com/commerce/extensibility/observability/)实例，该可观察性现在自动可用。 OpenTelemetry提供量度、日志和跟踪，帮助您监控性能、更快地排除问题以及优化店面。 此功能支持对系统运行状况进行主动分析，并提高了客户的可靠性。

>[!NOTE]
>
>OpenTelemetry可观察性要求使用[!DNL App Builder]或其他进程外可扩展性(OOPE)产品。

### 目录价格规则的分层定价

您现在可以使用[目录价格规则](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/pricing/product-price-tier#enable-tier-pricing-for-catalog-price-rules)将分层定价折扣与目录规则折扣相结合。 此增强功能允许您创建更动态、更有竞争力的定价策略 — 在奖励批量购买的同时应用促销折扣。 这样可以更灵活地吸引客户、增加订单价值并促进转化。<!-- See PR #708 in commerce-admin -->

### 增强功能和错误修复

此版本中包含以下选定的增强功能、优化和错误修复：

* 解决了将文件上传到S3时可能发生的错误。<!-- CCSAAS-4189 -->

* 解决了登录Commerce管理员或访问REST API时可能出现的`User is not entitled to access this instance`错误。<!-- CCSAAS-4324 -->

* 更正了在新闻稿模板网格中预览新闻稿或将新闻稿排队时发生的错误。<!-- CCSAAS-4398 -->

* 修复了单击管理员仪表板上的`404`重新加载数据&#x200B;[!UICONTROL **按钮时发生的**]&#x200B;错误。<!-- CCSAAS-4468 -->

* 解决了启用[!DNL AEM Assets integration]且产品具有图像时，无法通过REST API更新产品自定义属性的问题。<!-- ACAP-1178 -->

* 各种性能和优化改进。<!-- CCSAAS-4255 --><!-- CCSAAS-4233 --><!-- CCSAAS-4220 --><!-- CCSAAS-4252 --><!-- CCSAAS-4330 --><!-- CCSAAS-3669 --><!-- CCSAAS-4462 -->

{{accs-release}}

>[!ENDSHADEBOX]

## 2025年11

>[!BEGINSHADEBOX]

### 增强功能

* [用户管理](./user-management.md) — 更改了Admin Console中的&#x200B;**产品管理员**&#x200B;角色以自动更新用户对Commerce管理员的访问权限。<!-- CCSAAS-3012 -->

* 添加了使用[GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/uploads)和[REST](https://developer.adobe.com/commerce/webapi/rest/modules/s3-uploads)中的预签名URL将可协商的报价附件以及与客户和客户地址关联的文件和图像上传和检索到Amazon S3的功能。 使用REST，您还可以上传类别图像。<!-- CCSAAS-3250 -->

* 已将`POST /V1/customers`和`PUT /V1/customers/{customerId}`端点添加到[REST API](https://developer.adobe.com/commerce/webapi/rest/reference/)以创建和更新客户。 这些端点需要IMS授权。<!-- CCSAAS-3112 -->

* 添加了需要购物者的电子邮件地址和一次性密码(OTP)的[`exchangeOtpForCustomerToken`突变](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/exchange-otp-customer-token/)，并接收客户令牌以交换。 此突变通常用于客户需要使用发送到其电子邮件或电话的OTP进行身份验证的情况。

* 如果在Admin的&#x200B;[!UICONTROL **存储电子邮件地址**]&#x200B;配置屏幕中定义的某个地址包含以`example.com`结尾的值，则Commerce不会向此地址发送电子邮件。 相反，系统会记录未发送电子邮件。 <!-- CCSAAS-3533 -->

#### 自定义订单属性

* 管理员用户现在可以直接从“管理员”面板的“订单查看”、“编辑”和“创建”屏幕查看和编辑[自定义订单属性](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing#custom-order-attributes)。 此增强功能改进了通过GraphQL创建的自定义订单数据的管理。<!-- CEXT-5044 -->

>[!ENDSHADEBOX]
