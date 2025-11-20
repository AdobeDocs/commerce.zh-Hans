---
title: '[!DNL Adobe Commerce as a Cloud Service]发行说明'
description: 了解 [!DNL Adobe Commerce as a Cloud Service]中的最新功能和改进。
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Developer, User, Leader
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目(Adobe管理的SaaS基础架构)。"
exl-id: cf06dec6-8d6b-413e-9977-df88373c188e
source-git-commit: 925df19c2827f474efe85708ea49974b285df29e
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---

# 发行说明

以下发行说明包含[!DNL Adobe Commerce as a Cloud Service]的更新。 有关其他产品的发行信息，请参阅[Adobe Commerce Optimizer](../optimizer/release-notes.md)或[Adobe Commerce内部部署和Adobe Commerce on Cloud](https://experienceleague.adobe.com/en/docs/commerce-operations/release/notes/overview)。

[!DNL Adobe Commerce as a Cloud Service]包含最新版本的促销服务、支付服务和可扩展性版本。 请使用以下链接查看每个页面的发行说明：

* 服务
   * [目录服务](../catalog-service/release-notes.md)
   * [实时搜索](../live-search/release-notes.md)
   * [支付服务](../payment-services/release-notes.md)
   * [产品推荐](../product-recommendations/release-notes.md)
   * [SaaS数据导出](../data-export/release-notes.md)
* 可扩展性
   * [管理员UI SDK](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/release-notes/)
   * [API网格](https://developer.adobe.com/graphql-mesh-gateway/mesh/release)
   * [个事件](https://developer.adobe.com/commerce/extensibility/events/release-notes/)
   * [Webhooks](https://developer.adobe.com/commerce/extensibility/webhooks/release-notes/)

## 2025年11

>[!BEGINSHADEBOX]

### 增强功能

* [用户管理](./user-management.md) — 更改了Admin Console中的&#x200B;**产品管理员**&#x200B;角色以自动更新用户对Commerce管理员的访问权限。<!-- CCSAAS-3012 -->

* 添加了使用[GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/uploads)和[REST](https://developer.adobe.com/commerce/webapi/rest/modules/s3-uploads)中的预签名URL将可协商的报价附件以及与客户和客户地址关联的文件和图像上传和检索到Amazon S3的功能。 使用REST，您还可以上传类别图像。<!-- CCSAAS-3250 -->

* 已将`POST /V1/customers`和`PUT /V1/customers/{customerId}`端点添加到[REST API](https://developer.adobe.com/commerce/webapi/rest/reference/)以创建和更新客户。 这些端点需要管理员授权。<!-- CCSAAS-3112 -->

* 添加了需要购物者的电子邮件地址和一次性密码(OTP)的[`exchangeOtpForCustomerToken`突变](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/exchange-otp-customer-token/)，并接收客户令牌以交换。 此突变通常用于客户需要使用发送到其电子邮件或电话的OTP进行身份验证的情况。

* 如果在Admin的&#x200B;[!UICONTROL **存储电子邮件地址**]&#x200B;配置屏幕中定义的某个地址包含以`example.com`结尾的值，则Commerce不会向此地址发送电子邮件。 相反，系统会记录未发送电子邮件。 <!-- CCSAAS-3533 -->

#### 自定义订单属性

* 管理员用户现在可以直接从“管理员”面板的“订单查看”、“编辑”和“创建”屏幕查看和编辑[自定义订单属性](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing#custom-order-attributes)。 此增强功能改进了通过GraphQL创建的自定义订单数据的管理。<!-- CEXT-5044 -->

>[!ENDSHADEBOX]
