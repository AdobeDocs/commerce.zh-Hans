---
source-git-commit: 25e92d9418c5b0ac331e8aab2e13330f52ca85bb
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---
# Commerce代码片段

## ACCS早期访问 {#accs-early-access}

>[!NOTE]
>
>本文档描述了早期访问开发中的产品，并未反映用于正式发布的所有功能。

<!--
## Nav hack ACCS {#nav-hack-accs}

>[!BEGINSHADEBOX]

<table style="table-layout:fixed">
  <tr>
    <td style="vertical-align: middle;"><a href="https://developer.adobe.com/commerce/webapi/"><img alt="Developers" src="../assets/icons/developers.svg" /> <strong>Developers</strong></a></td>
    <td style="vertical-align: middle;"><a href="https://experienceleague.adobe.com/developer/commerce/storefront/?lang=zh-Hans"><img alt="Storefront" src="../assets/icons/storefront.svg" /> <strong>Storefront</strong></a></td>
    <td style="vertical-align: middle;"><a href="../cloud-service/overview.md"><img alt="Merchants" src="../assets/icons/merchants.svg" /> <strong>Merchants</strong></a></td>
    <td style="vertical-align: middle;"><a href="https://experienceleague.adobe.com/zh-hans/docs/commerce-learn/tutorials/getting-started/commerce-as-a-cloud-service/overview"><img alt="Videos" src="../assets/icons/videos.svg" /> <strong>Videos</strong></a></td>
    <td style="vertical-align: middle;"><a href="https://experienceleague.adobe.com/developer/commerce/storefront/playgrounds/commerce-services/?lang=zh-Hans"><img alt="Playgrounds" src="../assets/icons/playgrounds.svg" /> <strong>Playgrounds</strong></a></td>
  </tr>
</table>

>[!ENDSHADEBOX]
-->

## ACCS仅沙盒实验功能 {#accs-sandbox-experimental}

>[!IMPORTANT]
>
>此功能是试验性的，仅在[!DNL Adobe Commerce as a Cloud Service]的沙盒环境中可用。
>
>此功能可能会发生更改，恕不另行通知。

[!BADGE 沙盒]{type=Caution tooltip="列出的项目当前仅在沙盒环境中可用。 Adobe首先在沙盒环境中提供新版本，以便在该版本在生产环境中可用之前提供时间来测试即将进行的更改。"}

## AEM Assets实例映射 {#aem-assets-instance-mapping}

>[!NOTE]
>
>将[!DNL Adobe Commerce as a Cloud Service]连接到[!DNL AEM Assets]时，您的[!DNL AEM Assets]阶段实例将映射到您的沙盒[!DNL Adobe Commerce as a Cloud Service]实例和任何其他非生产环境。 您的[!DNL AEM Assets]生产实例映射到[!DNL Adobe Commerce as a Cloud Service]生产实例。

## IMS身份和单点登录信息 {#ims-identity-and-sso-config}

Adobe Commerce身份管理和身份验证由Adobe Identity Management System (IMS)通过Adobe Admin Console管理。

有关身份配置选项（包括Adobe ID、Enterprise ID和Federated ID）的信息，以及有关配置单点登录(SSO)以安全访问Adobe应用的说明，请参阅[企业Admin Console](https://helpx.adobe.com/cn/enterprise/using/set-up-identity.html)文档中的&#x200B;*设置身份和单点登录*。

## ACCS服务和可扩展性发行说明 {#accs-release}

### 其他发行说明

[!DNL Adobe Commerce as a Cloud Service]包含最新版本的促销服务、付款服务和可扩展性版本。 请使用以下链接查看每个页面的发行说明：

| 服务 | 可扩展性 | 店面 |
| --- | --- | --- |
| <ul><li>[目录服务](../catalog-service/release-notes.md)</li><li>[实时搜索](../live-search/release-notes.md)</li><li>[付款服务](../payment-services/release-notes.md)</li><li>[产品推荐](../product-recommendations/release-notes.md)</li><li>[SaaS数据导出](../data-export/release-notes.md)</li></ul> | <ul><li>[管理员UI SDK](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/release-notes/)</li><li>[API网格](https://developer.adobe.com/graphql-mesh-gateway/mesh/release)</li><li>[个事件](https://developer.adobe.com/commerce/extensibility/events/release-notes/)</li><li>[Webhooks](https://developer.adobe.com/commerce/extensibility/webhooks/release-notes/)</li></ul> | <ul><li>[版本信息](https://experienceleague.adobe.com/developer/commerce/storefront/releases/?lang=zh-Hans)</li><li>[更改日志](https://experienceleague.adobe.com/developer/commerce/storefront/releases/changelog/?lang=zh-Hans)</li></ul> |
