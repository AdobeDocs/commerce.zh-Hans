---
title: 验证迁移服务访问权限
description: 了解如何验证对Commerce数据迁移服务API的端到端访问权限，确认网络可达性、IMS身份验证和租户授权。
feature: Cloud
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目（Adobe管理的SaaS基础架构）。"
role: Developer
level: Intermediate
autotag-review: '2026-07-22T19:18:53.554Z'
TQID: 'https://experienceleague.adobe.com/csDq2Bbha2IieqxsDDG0iS1IHhAJ02fD-cwd8KFIsSk'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
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
source-wordcount: 452
ht-degree: 1%

---

# 验证迁移服务访问权限

{{bulk-data-early-access}}

使用本指南验证从您的环境对Commerce数据迁移服务(CDMS) API的端到端访问权限。 成功的调用将同时验证来自您的出口IP（IP身份验证）、IMS身份验证和租户授权的网络可达性。

完成[客户准备工作清单](readiness-checklist.md)中的所有项目后，在运行[迁移指南](migration-guide.md)中描述的迁移之前，请完成本指南。

## 先决条件

- 在[Adobe Developer Console](https://developer.adobe.com/console/)中创建的OAuth 2.0服务器到服务器凭据（客户端ID和客户端密钥）。
- 您的IMS组织ID，格式为`<org>@AdobeOrg`。 组织必须拥有目标租户。
- 目标`tenantId`，22个字符，字母数字IMS租户ID。
- 向Adobe提交并由为CDMS网关列入允许列表的出站出口IP地址。 如果您不确定IP地址或其状态，请与Adobe团队协调。
- [服务中特定于区域的服务主机（按环境和区域](#service-hosts-by-environment-and-region)表）。

## 生成IMS访问令牌

使用授予`client_credentials`的OAuth 2.0服务器到服务器凭据生成访问令牌。 此步骤中的IMS主机对于所有数据区域都是相同的。 只有CDMS主机会按区域进行更改。

```bash
curl -X POST "https://ims-na1.adobelogin.com/ims/token/v3" \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -H "x-org-id:<your-org-id>@AdobeOrg" \
  -d "grant_type=client_credentials" \
  -d "client_id=<your-ims-client-id>" \
  -d "client_secret=<your-ims-client-secret>" \
  -d "scope=AdobeID,openid,read_organizations,additional_info.projectedProductContext,additional_info.roles,adobeio_api,read_client_secret,manage_client_secrets"
```

## 调用列表迁移API

以下请求检索租户的迁移列表，并需要上一步骤中的访问令牌。 从[按环境和区域](#service-hosts-by-environment-and-region)列出的服务主机中选择您所在区域的主机。 `-i`标记会打印HTTP状态行和响应标头，以便您确认结果。

```bash
curl -i "https://<host>/<tenantId>/v1/migrations" \
  -H "Authorization: Bearer <your IMS access token>"
```

## 解释响应

| HTTP代码 | 含义 | 示例响应正文 |
| --- | --- | --- |
| 200 | 成功。 连接、身份验证和租户授权都通过。 响应正文包含租户的迁移列表。 | `{"migrations":[...]}` |
| 401 | 持有者令牌缺失或无效，在访问服务之前被拒绝。 [重新生成令牌](#generate-an-ims-access-token)。 | 不尽相同（网关生成） |
| 403 | 经过身份验证的用户没有此租户的迁移权限。 | `{"error":"access_denied","message":"You do not have permission to access this tenant"}` |
| 500 | 内部服务器错误。 | `{"error":{"message":"Internal Server Error","status":500}}` |

>[!NOTE]
>
>如果请求超时或连接被拒绝，并且未返回HTTP状态，则可能是您的出口IP未，或者您使用的主机不正确。 确认下表中的区域主机和列入允许列表的IP。

## 按环境和地区划分的服务主机

| 区域或环境 | 主机 |
| --- | --- |
| 沙盒或预生产 | `https://na1-sandbox.api.commerce.adobe.com` |
| 北美 | `https://na1.api.commerce.adobe.com` |
| 欧洲 | `https://eu1.api.commerce.adobe.com` |
| 印度 | `https://in1.api.commerce.adobe.com` |
| UK | `https://uk1.api.commerce.adobe.com` |
| 澳大利亚和新西兰 | `https://au1.api.commerce.adobe.com` |

## 后续步骤

确认访问后，请继续阅读[迁移指南](migration-guide.md)以开始环境配置和迁移执行。
