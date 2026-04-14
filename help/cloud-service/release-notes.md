---
title: '[!DNL Adobe Commerce as a Cloud Service]发行说明'
description: 了解 [!DNL Adobe Commerce as a Cloud Service]中的最新功能和改进。
feature-set: Commerce
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Developer, User, Leader
level: Beginner
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目（Adobe管理的SaaS基础架构）。"
exl-id: cf06dec6-8d6b-413e-9977-df88373c188e
source-git-commit: 848d8501c974711c42926835cb4f4488bd387d53
workflow-type: tm+mt
source-wordcount: '2519'
ht-degree: 0%

---

# 发行说明

以下发行说明包含[!DNL Adobe Commerce as a Cloud Service]的更新。

>[!NOTE]
>
>如果您正在本地使用Adobe Commerce或在云基础架构上使用Adobe Commerce，请参阅[Adobe Commerce发行说明](https://experienceleague.adobe.com/en/docs/commerce-operations/release/notes/overview)。

## 2026年4月 — 发行说#2 {#latest}

<!-- [!BADGE Production]{type=Neutral tooltip="The items listed are currently available in Production environments."} -->

[!BADGE 沙盒]{type=Caution tooltip="列出的项目当前仅在沙盒环境中可用。 Adobe首先在沙盒环境中提供新版本，以便在该版本在生产环境中可用之前提供时间来测试即将进行的更改。"}

以下项目将于2026年4月16日发布到生产环境。

>[!BEGINSHADEBOX]

### 使用Webhook实施自定义报价总计

`plugin.magento.out_of_process_totals_collector.api.get_total_modifications.execute` [webhook](https://developer.adobe.com/commerce/extensibility/webhooks/)现在可在[!DNL Adobe Commerce as a Cloud Service]中使用。 使用它通过超出流程的可扩展性实施自定义报价总额修改。<!-- CEXT-5896 -->

### 查看“付款服务交易记录”报表

如果您启用了[[!DNL Payment Services]](https://experienceleague.adobe.com/en/docs/commerce/payment-services/get-started/production)，则[仪表板UI](../payment-services/payments-home.md)现在可在[!DNL Commerce Admin]中使用，从而提供对[交易报表](../payment-services/reporting.md#transactions-report-view)的访问权限，以便查看和管理付款交易。<!-- PAY-6510 -->

### 增强功能和错误修复

此版本中包含以下选定的增强功能、优化和错误修复：

* 修复了“共享目录分配公司”页面上的500错误，该错误会在将大型共享目录与管理UI SDK结合使用时出现。<!-- CCSAAS-4783 -->

* 修复了以下问题：如果在将客户分配给公司之前下达了公司客户自己的订单，则公司客户将无法看到这些订单。<!-- ACCS-746 -->

{{accs-release}}

>[!ENDSHADEBOX]

## 2026年4月

[!BADGE 生产]{type=Neutral tooltip="列出的项目当前在生产环境中可用。"}

以下项目已于2026年4月1日发布到生产环境。

>[!BEGINSHADEBOX]

### 将文件添加到产品

[!DNL Adobe Commerce as a Cloud Service]现在支持使用文件类型产品属性[将文件添加到产品](./product-files.md)。 您可以在产品编辑页面上手动上传文件，或者通过REST API以编程方式上传，也可以通过CSV提供外部URL批量上传。<!-- ACCS-535, ACCS-565 -->

### 通过GraphQL检查价格和股票提醒订阅状态

新的GraphQL查询[`isSubscribedProductAlertStock`](https://developer.adobe.com/commerce/webapi/graphql/schema/products/queries/is-subscribed-product-alert-stock/){target="_blank"}和[`isSubscribedProductAlertPrice`](https://developer.adobe.com/commerce/webapi/graphql/schema/products/queries/is-subscribed-product-alert-price/){target="_blank"}让店面确定购物者是否已订阅产品的库存或价格警报。<!-- ACCS-334 -->

### 创建支持负值的数字产品属性

新的`numeric` [产品属性输入类型](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/attributes-input-types)允许商家创建支持负值的十进制属性。<!-- ACCS-600 -->

### 在一个GraphQL请求中查询多个表单的reCAPTCHA配置

[`recaptchaFormConfigs`查询](https://developer.adobe.com/commerce/webapi/graphql/schema/store/queries/recaptcha-form-configs/)可以在单个请求中返回多个表单类型的配置详细信息。<!-- ACCS-628 -->

### 查看具有新B2B权限的所有公司订单

新的`view_all_company_orders` [公司角色](https://developer.adobe.com/commerce/webapi/rest/b2b/roles/)允许B2B公司客户查看其公司内的所有订单，包括管理员用户创建的历史订单。<!-- ACCS-675 -->

### 增强功能和错误修复

此版本中包含以下选定的增强功能、优化和错误修复：

* 您现在可以使用适用的自定义属性来筛选订单和公司REST API结果，支持公司范围的订单搜索等方案。<!-- ACCS-633 -->

* 解决了可能显示在浏览器开发人员控制台中的错误。<!-- CCSAAS-4650 -->

* 修复了在取消带有订单注释的访客订单时可能发生的错误。<!-- ACCS-674 -->

* 修复了在将具有多个关联项的分组产品添加到申请列表时可能发生的错误。<!-- ACCS-627 -->

>[!ENDSHADEBOX]

## 2026年3月 — 发行说#2

[!BADGE 生产]{type=Neutral tooltip="列出的项目当前在生产环境中可用。"}

以下项目已于2026年3月24日发布到生产环境。

>[!BEGINSHADEBOX]

### 使用一次性代码以客户身份登录

管理员现在可以通过[和REST API生成客户模拟的](https://experienceleague.adobe.com/en/docs/commerce-admin/customers/customer-accounts/manage/login-as-customer)一次性代码[!DNL Commerce Admin]。 可以通过`generateCustomerToken`或`exchangeOtpForCustomerToken`GraphQL突变为客户访问令牌交换一次性代码，从而支持无密码的“以客户身份登录”流程用于卖方辅助购物方案。<!-- ACCS-404 -->

有关使用API实施此功能的指导，请参阅[REST API](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/login-as-customer/)和[GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/generate-token/)文档。

### 通过REST API管理礼品卡帐户

现在可以通过REST API创建、更新、删除和查询[礼品卡帐户](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/gift-card-accounts/)。 此外，通过`/V1/import/json`端点提供JSON批量导入支持，从而支持第三方集成以编程方式同步礼品卡。<!-- ACCS-476 -->

### 通过REST API触发事务性电子邮件

新的REST API端点(`POST /V1/custom-email/send`)允许您通过指定电子邮件模板ID、收件人电子邮件和模板变量，按需[触发事务性电子邮件](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/custom-email/)。 该API支持将嵌套数组作为复杂电子邮件内容的模板变量。<!-- ACCS-325, ACCS-481 -->

### 订阅进程外送货获取费率webhook

`plugin.out_of_process_shipping_methods.api.shipping_rate_repository.get_rates` webhook现在可在[!DNL Adobe Commerce as a Cloud Service]的Admin Webhook列表中使用。 使用它实施[自定义送货方法](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/shipping-use-cases/#shipping-methods)。<!-- ACCS-478 -->

### 通过产品属性上传PDF和其他文件

新的“文件”[属性输入类型](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/attributes-input-types)允许您创建属性集，您可以在其中将文件（如PDF）上传到各个产品。 您可以通过导航到&#x200B;[!UICONTROL **商店**] > [!UICONTROL **配置**] > [!UICONTROL _目录_] > [!UICONTROL **产品文件属性**]，配置允许的文件扩展名和最大文件大小。<!-- ACCS-535, ACCS-565 -->

### 配置公司自定义属性

管理员现在可以在[!DNL Commerce Admin]的公司编辑页面上管理公司自定义属性。 可以从[!DNL Adobe Commerce as a Cloud Service]的管理界面配置、保存和验证自定义属性。

要配置公司自定义属性，请导航到&#x200B;[!UICONTROL **客户**] > [!UICONTROL **公司**]，然后选择一个公司以打开编辑页面。 然后选择&#x200B;[!UICONTROL **自定义属性**]&#x200B;选项卡以添加新属性。
<!-- ACCS-294 -->

### 通过GraphQL订阅价格和股票警报

EDS店面现在使用[价格和库存警报](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/configuration/product-alerts/alert-setup)。<!-- ACCS-334 -->

此外，还有几个新的GraphQL突变可用来订阅和取消订阅价格和股票警报：

+++新的GraphQL突变

```graphql
mutation {
  subscribeProductAlertStock(input: { sku: "ADB111" }) {
    success
    message
  }
}
```

```graphql
mutation {
  unsubscribeProductAlertStock(input: { sku: "ADB111" }) {
    success
    message
  }
}
```

```graphql
mutation {
  unsubscribeProductAlertStockAll {
    success
    message
  }
}
```

```graphql
mutation {
  subscribeProductAlertPrice(input: { sku: "ADB112" }) {
    success
    message
  }
}
```

```graphql
mutation {
  unsubscribeProductAlertPrice(input: { sku: "ADB115" }) {
    success
    message
  }
}
```

```graphql
mutation {
  unsubscribeProductAlertPriceAll {
    success
    message
  }
}
```

+++

### 增强功能和错误修复

此版本中包含以下选定的增强功能、优化和错误修复：

* [!UICONTROL Sales] > [!UICONTROL View Orders]公司角色现在按预期运行。<!-- ACCS-604 -->

* `last_login_at`客户扩展属性现在可通过REST API使用，从而支持集成检索每位客户的最新登录日期。<!-- ACCS-555 -->

* 修复了[!DNL AEM Assets]集成表单建议的问题。<!-- ACCS-209 -->

* 修复了共享目录网格上的批量公司分配和取消分配操作可能会导致错误的问题。<!-- CCSAAS-4614 -->

* 修复了在将同一产品再次以不同的数量或自定义价格添加到购物车时覆盖自定义购物车定价的问题。<!-- ACCS-529 -->

* 申请列表物料UID现在与购物车和愿望清单物料UID一致。<!-- ACCS-349 -->

* 修复了在大型共享目录下可能发生的产品编辑页面超时问题。<!-- CCSAAS-4657 -->

* 为管理员集成重新启用GET `/V1/directory/countries`和GET `/V1/directory/countries/:countryId` REST API端点，允许客户端查找有效的国家/地区数据。<!-- ACCS-518 -->

* 修复了当用户拥有大型共享目录时，REST API中可能发生的超时问题。<!-- ACCS-4657 -->

* 修复了被阻止的B2B公司仍可以向购物车添加产品的问题。<!-- ACCS-552 -->

* 如果“客户”或“公司”网格中有大量数据，则无法再使用导出按钮来防止出现错误。<!-- ACCS-320 -->

* 修复了附加文件大小显示不正确的问题。<!-- ACCS-566 -->

* 修复了在[!DNL Commerce Admin]中创建和删除“File”属性类型时出现的问题。<!-- ACCS-605, ACCS-606 -->

>[!ENDSHADEBOX]


## 2026年3月 — 发行说#1

[!BADGE 生产]{type=Neutral tooltip="列出的项目当前在生产环境中可用。"}

以下项目已于2026年3月9日发布到[!DNL Adobe Commerce as a Cloud Service]的生产环境。

>[!BEGINSHADEBOX]

### App Builder AI编码工具和教程

您现在可以使用[AI编码开发人员工具](https://developer.adobe.com/commerce/extensibility/developer-agent/){target="_blank"}创建新的[!DNL App Builder]应用程序并将现有[!DNL Adobe Commerce] PHP扩展转换为[!DNL App Builder]应用程序。 以下教程将演示这些工具的使用方法：

* [教程先决条件](./tutorials/tutorial-prerequisites.md)
* [评级扩展教程](./tutorials/ratings-extension.md)
* [配送方法扩展教程](./tutorials/shipping-method-extension.md)

### 通过管理员访问App Builder应用程序管理

[!DNL Commerce Admin]现在包含一个链接到[应用程序管理](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"}的菜单项，这是一个统一的Shell，用于管理与Commerce实例关联的[!DNL App Builder]个应用程序。 此添加由最新的Admin UI SDK更新提供支持。<!-- CEXT-5755 -->

### 请求实体创建限制更改

网站、商店和商店查看次数的限制以前限制为50。 如有必要，您现在可以提交[支持请求](https://experienceleague.adobe.com/home?support-tab=home#support)以修改这些限制。<!-- ACCS-398 -->

### 使用结构化错误代码自定义店面身份验证消息

[`generateCustomerToken` GraphQL突变](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/generate-token/){target="_blank"}现在会随错误消息一起返回键入的错误代码，使店面能够按失败原因显示特定的UI消息。 可用的错误代码包括： `CUSTOMER_MISSING_EMAIL`、`CUSTOMER_MISSING_PASSWORD`、`CUSTOMER_SIGN_IN_INCORRECT_OR_LOCKED`、`CUSTOMER_ACCOUNT_NOT_CONFIRMED`和`CUSTOMER_GENERIC_ERROR`。<!-- ACCS-301 -->

### 发送有关购物车和愿望清单不活动的自动电子邮件提醒

[电子邮件提醒模块](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/communications/email-reminders/email-reminder-rules) (`Magento_Reminder`)现在在[!DNL Adobe Commerce as a Cloud Service]中处于活动状态，允许商家创建自动提醒规则，以根据购物车和愿望清单非活动状态触发发送给客户的电子邮件。<!-- CCSAAS-4597 -->

### 订阅类别删除事件webhook

`observer.catalog_category_delete_before` webhook现在可在[!DNL Adobe Commerce as a Cloud Service]中使用。 使用它可在删除类别之前运行逻辑。<!-- CEXT-5862 -->

### 跟踪在注册电子邮件中下单的访客订单

新的可选商店级别配置允许客户[跟踪他们发出的访客订单](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/point-of-purchase/checkout/checkout-guest#allow-guest-order-access-for-registered-emails)（如果订单的电子邮件地址与已注册的客户帐户匹配）。<!-- ACCS-289 -->

### 增强功能和错误修复

此版本中包含以下选定的增强功能、优化和错误修复：

* 修复了以下问题：某些组织管理员在没有每个租户权利的情况下可能错误地访问租户实例。<!-- ACCS-335 -->

* 修复了在更改共享目录时可能导致用户从[!DNL Commerce Admin]中注销的问题。<!-- ACCS-318 -->

* 修复了导致某些Webhook字段在[!DNL Commerce Admin] UI中显示不正确的问题。<!-- CEXT-5874 -->

>[!ENDSHADEBOX]

## 2026年2月 — 发行说#2

[!BADGE 生产]{type=Neutral tooltip="列出的项目当前在生产环境中可用。"}

以下项目已于2026年2月24日发布到[!DNL Adobe Commerce as a Cloud Service]的生产环境。

>[!BEGINSHADEBOX]

### 使用商务事件发送上下文字段

[!DNL Adobe Commerce as a Cloud Service]现在在事件负载中支持[上下文字段](https://developer.adobe.com/commerce/extensibility/events/context-fields/)，从而允许您包含默认情况下不属于事件的数据。<!-- CEXT-5713 -->

### 使用新的webhook订阅报价项保存事件

`observer.sales_quote_item_save_before` webhook现在可在[!DNL Adobe Commerce as a Cloud Service]中使用。 在保存报价项之前，使用它来运行逻辑。<!-- ACCS-346 -->

### 增强功能和错误修复

此版本中包含以下选定的增强功能、优化和错误修复：

* 修复了可能导致[!DNL Commerce Admin]产品列表中的显示问题的错误。 现在，产品列表限制了为提高性能而显示的共享目录的数量。<!-- CCSAAS-1242 -->

* 修复了可能阻止将可自定义的礼品卡添加到购物车的GraphQL错误。<!-- ACCS-313 -->

>[!ENDSHADEBOX]

## 2026年2月 — 发行说#1

[!BADGE 生产]{type=Neutral tooltip="列出的项目当前在生产环境中可用。"}

以下项目已于2026年2月10日发布到[!DNL Adobe Commerce as a Cloud Service]的生产环境。

>[!BEGINSHADEBOX]

### 自定义配送方式并查看管理员报表

对[!DNL Commerce Admin]进行了以下增强：

* 增强了进程外[送货webhook负载](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/shipping-use-cases/#payload)以包含送货地址自定义属性。 这项更改使商家能够实施自定义配送方式。<!-- ACCS-235 -->

* 已添加对管理员报告的访问权限，这些报告包括[客户](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/customer-reports)、[营销](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/marketing-reports)、[产品](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/product-reports)和[销售](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/sales-reports)的报告。<!-- CCSAAS-3085 -->

>[!NOTE]
>
>[!DNL Adobe Commerce as a Cloud Service]中不可用的报告仅标记为PaaS （[!BADGE 仅PaaS ]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于云项目（Adobe管理的PaaS基础架构）和内部部署项目上的Adobe Commerce 。"}）。

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

您现在可以使用[目录价格规则](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/pricing/product-price-tier#enable-tier-pricing-for-catalog-price-rules)将分层定价折扣与目录规则折扣相结合。 此增强功能允许您创建更动态、更有竞争力的定价策略，在奖励批量购买的同时应用促销折扣。 这样可以更灵活地吸引客户、增加订单价值并促进转化。<!-- See PR #708 in commerce-admin -->

### 增强功能和错误修复

此版本中包含以下选定的增强功能、优化和错误修复：

* 解决了将文件上传到S3时可能发生的错误。<!-- CCSAAS-4189 -->

* 解决了登录Commerce管理员或访问REST API时可能出现的`User is not entitled to access this instance`错误。<!-- CCSAAS-4324 -->

* 更正了在新闻稿模板网格中预览新闻稿或将新闻稿排队时发生的错误。<!-- CCSAAS-4398 -->

* 修复了单击管理员仪表板上的`404`重新加载数据&#x200B;[!UICONTROL **按钮时发生的**]&#x200B;错误。<!-- CCSAAS-4468 -->

* 解决了启用[!DNL AEM Assets integration]且产品具有图像时，无法通过REST API更新产品自定义属性的问题。<!-- ACAP-1178 -->

* 各种性能和优化改进。<!-- CCSAAS-4255 --><!-- CCSAAS-4233 --><!-- CCSAAS-4220 --><!-- CCSAAS-4252 --><!-- CCSAAS-4330 --><!-- CCSAAS-3669 --><!-- CCSAAS-4462 -->

>[!ENDSHADEBOX]

## 2025年11

>[!BEGINSHADEBOX]

### 增强功能

* [用户管理](./user-management.md) — 更改了Admin Console中的&#x200B;**产品管理员**&#x200B;角色以自动更新用户对Commerce管理员的访问权限。<!-- CCSAAS-3012 -->

* 添加了使用[GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/uploads)和[REST](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/s3-uploads)中的预签名URL将可协商的报价附件以及与客户和客户地址关联的文件和图像上传和检索到Amazon S3的功能。 使用REST，您还可以上传类别图像。<!-- CCSAAS-3250 -->

* 已将`POST /V1/customers`和`PUT /V1/customers/{customerId}`端点添加到[REST API](https://developer.adobe.com/commerce/webapi/rest/reference/)以创建和更新客户。 这些端点需要IMS授权。<!-- CCSAAS-3112 -->

* 添加了需要购物者的电子邮件地址和一次性密码(OTP)的[`exchangeOtpForCustomerToken`突变](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/exchange-otp-customer-token/)，并接收客户令牌以交换。 此突变通常用于客户需要使用发送到其电子邮件或电话的OTP进行身份验证的情况。

* 如果在Admin的&#x200B;[!UICONTROL **存储电子邮件地址**]&#x200B;配置屏幕中定义的某个地址包含以`example.com`结尾的值，则Commerce不会向此地址发送电子邮件。 相反，系统会记录未发送电子邮件。 <!-- CCSAAS-3533 -->

#### 自定义订单属性

* 管理员用户现在可以直接从“管理员”面板的“订单查看”、“编辑”和“创建”屏幕查看和编辑[自定义订单属性](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing#custom-order-attributes)。 此增强功能改进了通过GraphQL创建的自定义订单数据的管理。<!-- CEXT-5044 -->

>[!ENDSHADEBOX]
