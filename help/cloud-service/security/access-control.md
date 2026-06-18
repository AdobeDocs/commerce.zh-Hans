---
title: 身份和访问管理
description: 了解Adobe Commerce as a Cloud Service的标识和访问管理功能。
role: Admin, Developer, Leader
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目（Adobe管理的SaaS基础架构）。"
autotag-review: '2026-06-18T16:14:06.699Z'
TQID: 'https://experienceleague.adobe.com/lbI3nsLtafel6GtquXnkZmXD2Z3b-rRGPOyr8EqzrjE'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: b5f00040-57a0-4a6d-a39e-383b1936c2c9
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
subfeature_v2:
  - id: e126554b-28f9-4290-b58c-10b888b88174
role_v2:
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: d378ca77-2da1-4f39-ad92-1917fe974a38
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adeb
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 15a99ce130efaf3a35968cfc01747fe1b6ab93c9
workflow-type: tm+mt
source-wordcount: 419
ht-degree: 0%

---


# 身份和访问管理

[!DNL Adobe Commerce as a Cloud Service]利用Adobe的企业级身份基础结构确保所有环境中的安全、可扩展和集中的访问控制。 [!DNL Adobe Commerce as a Cloud Service]中的身份和访问管理(IAM)旨在简化用户设置、强制最低权限访问并支持符合全局安全标准。

- **[!DNL Adobe Identity Management Services (IMS)]**： [!DNL Adobe Commerce as a Cloud Service]使用[Adobe Identity Management Services (IMS)](https://experienceleague.adobe.com/en/docs/commerce-admin/start/admin/ims/adobe-ims-integration-overview)对用户进行身份验证并管理权限。 这包括支持联合身份提供程序和[基于角色的访问控制](../user-management.md)。

- **Admin Console管理**：管理员通过[!DNL Adobe Admin Console]管理对店面和后端的访问。 权限可以将范围限定为特定功能和角色，以确保最低权限访问。

## Adobe Identity Management Services (IMS)

[!DNL Adobe Commerce as a Cloud Service]使用[!DNL Adobe Identity Management Services (IMS)]跨平台对用户进行身份验证和管理权限。 IMS提供：

- **联合身份支持**：使用SAML或OIDC与企业身份提供程序（如Azure AD和Okta）集成。
- **单点登录(SSO)**：无缝访问[!DNL Adobe Commerce]和其他[!DNL Adobe Experience Cloud]产品。
- **多重身份验证(MFA)**：已在组织级别强制实施以增强安全性。
- **全局冗余**：标识数据存储在多区域、负载平衡的云基础架构中。

## Admin Console访问控制

[!DNL Adobe Admin Console]是管理[!DNL Adobe Commerce as a Cloud Service]的用户访问权限的中心中心：

- **基于角色的访问控制(RBAC)**：根据用户的角色（如开发人员、管理员和分析人员）为用户分配粒度权限。
- **产品配置文件**：为不同的环境（如暂存环境和生产环境）定义访问范围。
- **委托管理**：系统管理员和产品管理员可以管理用户访问权限，而无需IT部门的介入。

有关详细信息，请参阅[用户管理](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/user-management)。

## API身份验证和集成安全性

使用标准化的OAuth 2协议通过Adobe的[!DNL Adobe Identity Management Services (IMS)]处理[!DNL Adobe Commerce as a Cloud Service]的REST API身份验证。 此身份验证系统支持基于用户的交互式工作流和自动化的服务器到服务器集成，确保不同用例的安全且适当的访问。

>[!NOTE]
>
>SaaS环境中不支持[!DNL Adobe Commerce]的PaaS版本中的管理和集成令牌生成方法。 相反，您必须通过OAuth身份验证获取IMS管理员令牌。

- **OAuth 2.0支持**：集成和第三方服务的基于安全令牌的身份验证。
- **作用域API访问**：限制API访问特定资源和操作。
- **审核日志记录**：跟踪身份验证事件并访问合规性和疑难解答的更改。

有关详细信息，请参阅[REST身份验证](https://developer.adobe.com/commerce/webapi/rest/authentication/)。
