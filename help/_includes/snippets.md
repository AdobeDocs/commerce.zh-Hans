---
source-git-commit: 156ed7a480de9239843c96b6b6bc252585f498d6
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---
# Commerce代码片段


## Optimizer的促销服务 {#aco-merchandising-services}

>[!NOTE]
>
>对于使用Adobe Commerce Optimizer或Adobe Commerce Optimizer连接器的Commerce解决方案，请使用[促销服务GraphQL API](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api/)，而不是目录服务GraphQL API。

## Optimizer的数据同步检查 {#aco-data-sync-verification}

>[!NOTE]
>
>如果您已安装[Adobe Commerce Optimizer Connector](../aco-connector/overview.md)以将目录数据导出到Adobe Commerce Optimizer，请使用Commerce Optimizer Studio中的[数据馈送同步状态页面](../optimizer/setup/data-sync.md)来检查是否已成功同步到Adobe Commerce Optimizer的数据，而不是数据管理功能板。

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
    <td style="vertical-align: middle;"><a href="https://experienceleague.adobe.com/developer/commerce/storefront/"><img alt="Storefront" src="../assets/icons/storefront.svg" /> <strong>Storefront</strong></a></td>
    <td style="vertical-align: middle;"><a href="../cloud-service/overview.md"><img alt="Merchants" src="../assets/icons/merchants.svg" /> <strong>Merchants</strong></a></td>
    <td style="vertical-align: middle;"><a href="https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/getting-started/commerce-as-a-cloud-service/overview"><img alt="Videos" src="../assets/icons/videos.svg" /> <strong>Videos</strong></a></td>
    <td style="vertical-align: middle;"><a href="https://experienceleague.adobe.com/developer/commerce/storefront/playgrounds/commerce-services/"><img alt="Playgrounds" src="../assets/icons/playgrounds.svg" /> <strong>Playgrounds</strong></a></td>
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

有关身份配置选项（包括Adobe ID、Enterprise ID和Federated ID）的信息，以及有关配置单点登录(SSO)以安全访问Adobe应用的说明，请参阅&#x200B;*企业Admin Console*&#x200B;文档中的[设置身份和单点登录](https://helpx.adobe.com/enterprise/using/set-up-identity.html)。

## ACCS服务和可扩展性发行说明 {#accs-release}

### 其他发行说明

[!DNL Adobe Commerce as a Cloud Service]包含最新版本的促销服务、付款服务和可扩展性版本。 请使用以下链接查看每个页面的发行说明：

| 服务 | 可扩展性 | 店面 |
| --- | --- | --- |
| <ul><li>[目录服务](../catalog-service/release-notes.md)</li><li>[实时搜索](../live-search/release-notes.md)</li><li>[付款服务](../payment-services/release-notes.md)</li><li>[产品推荐](../product-recommendations/release-notes.md)</li><li>[SaaS数据导出](../data-export/release-notes.md)</li></ul> | <ul><li>[管理员UI SDK](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/release-notes/)</li><li>[API网格](https://developer.adobe.com/graphql-mesh-gateway/mesh/release)</li><li>[个事件](https://developer.adobe.com/commerce/extensibility/events/release-notes/)</li><li>[Webhooks](https://developer.adobe.com/commerce/extensibility/webhooks/release-notes/)</li></ul> | <ul><li>[版本信息](https://experienceleague.adobe.com/developer/commerce/storefront/releases/)</li><li>[更改日志](https://experienceleague.adobe.com/developer/commerce/storefront/releases/changelog/)</li></ul> |

## Adobe Commerce Optimizer服务发行说明 {#aco-release}

### 其他发行说明

[!DNL Adobe Commerce Optimizer]使用最新版本的AEM Assets集成、Commerce Optimizer连接器和[!DNL Adobe Commerce Storefront]。 请使用以下链接查看每个区域的发行说明：

| 服务 | 店面 |
| --- | --- |
| [AEM Assets集成](../aem-assets-integration/release-notes.md)<br>[Commerce Optimizer连接器](../aco-connector/release-notes.md) | [店面版本信息](https://experienceleague.adobe.com/developer/commerce/storefront/releases/)<br>[店面变更日志](https://experienceleague.adobe.com/developer/commerce/storefront/releases/changelog/) |
