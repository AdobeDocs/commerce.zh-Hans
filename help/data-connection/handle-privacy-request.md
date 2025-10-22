---
title: ' [!DNL Commerce] 服务如何处理隐私请求'
description: 了解 [!DNL Commerce] 服务如何处理访问和删除数据的请求。
role: Admin, Leader
feature: Security, Compliance
exl-id: 1408ca77-6956-4519-93a6-bc9be9bffeff
source-git-commit: 5dd290a4e10bdbd1f6c96b67ab6c9ba1598705dc
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# 隐私请求

Adobe Experience Platform Privacy Service提供RESTful API和用户界面，帮助您管理客户数据请求。 借助Privacy Service，您可以提交从Adobe Experience Cloud应用程序访问和删除个人客户数据的请求，从而促进自动遵守法律和组织隐私法规。

有关Privacy Service以及如何创建和管理隐私请求的更多信息，请参阅Adobe Experience Platform文档：

* [Privacy Service概述](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/privacy/home)
* [在Privacy Service UI中管理隐私作业](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/privacy/ui/user-guide)

## 管理个人数据隐私请求

您可以通过两种方式提交单个请求以从[!DNL Commerce]访问和删除使用者数据：

* 通过&#x200B;**Privacy Service UI**。 请参阅文档[此处](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/privacy/ui/user-guide#_blank)。
* 通过&#x200B;**Privacy Service API**。 请参阅文档[此处](https://developer.adobe.com/experience-platform-apis/references/privacy-service/#_blank)和API信息[此处](https://developer.adobe.com/experience-platform-apis/#_blank)。

Privacy Service支持两种类型的请求：**数据访问**&#x200B;和&#x200B;**数据删除**。

>[!NOTE]
>
>本文重点介绍[!DNL Commerce]的隐私请求。 如果您计划为[Platform Data Lake](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/catalog/privacy)、[Real-Time Customer Profile](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/profile/privacy)或[Identity Service](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/identity/privacy)提出隐私请求，请参阅其各自的用户指南。 请注意，删除和访问请求必须单独向每个系统发出，因为向Commerce发出的隐私请求不会删除所有这些系统中的数据。

## 数据访问

对于&#x200B;**访问请求**，从UI中指定“Commerce (Personalization)”（或`commerceMarketingData`作为API中的产品代码）。

## 数据删除

对于删除请求，Privacy Service出于营销目的删除存储在Commerce SaaS服务中的[!DNL Commerce]数据，这意味着数据主体的配置文件和订单不再发送到Adobe营销应用程序以用于营销活动和客户历程。 但是，Privacy Service不会删除[!DNL Commerce]应用程序中的数据，因为商家事务型需求可能需要这些数据。 商家负责[!DNL Commerce]应用程序中的任何数据删除/访问请求。 请参阅[共享责任安全和运营模型](https://experienceleague.adobe.com/zh-hans/docs/commerce-operations/security-and-compliance/shared-responsibility)以了解详情。

[!DNL Commerce]将通过向商家发送请求删除特定数据的数据主体的信息来通知他们有关删除请求的信息。

## 如何创建访问和删除请求

### 先决条件

要请求访问和删除Adobe [!DNL Commerce]的数据，您必须拥有：

* IMS组织ID
* 要对其执行操作的人员和相应命名空间的身份标识符。 有关Adobe [!DNL Commerce]和Experience Platform中身份命名空间的更多信息，请参阅[身份命名空间概述](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/identity/features/namespaces)。

### GDPR请求/删除访问示例：

对于&#x200B;**访问请求**，从UI中指定“Commerce (Personalization)”（或“commerceMarketingData”作为API中的产品代码）。

对于&#x200B;**删除请求**，请确保启用“Commerce (Personalization)”复选框。 此外，如果客户配置文件和订单数据已从[!DNL Commerce]发送到Adobe Experience Platform，则必须向以下下游服务提交删除请求。

* 配置文件（产品代码：“profileService”）
* AEP Data Lake （产品代码：“AdobeCloudPlatform”）
* 标识（产品代码：“标识”）

要通过隐私API发送访问和删除请求，您必须对Privacy Service的权限进行身份验证和管理：

* [验证和访问Privacy Service API](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/privacy/api/getting-started)
* [管理Privacy Service的权限](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/privacy/permissions)

**必需的标头**

```bash
curl --location --request POST 'https://platform.adobe.io/data/core/privacy/jobs' \
--header 'Content-Type: application/json' \
--header 'x-api-key: {{CLIENT_ID}}' \
--header 'x-gw-ims-org-id: {{IMS_ORGID}}' \
--header 'Authorization: Bearer {{ACCESS_TOKEN}}' \
```

**请求**

```json
{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{{IMS_ORGID}}"
      }
    ],
    "users": [
      {
        "key": "sampleUserKey1",
        "action": ["access"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "dsmith@sample.com",
            "type": "standard"
          }
        ]
      },
      {
        "key": "sampleUserKey2",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "ajones@sample.com",
            "type": "standard"
          }
        ]
      }
    ],
    "include": ["commerceMarketingData"],
    "expandIds": false,
    "priority": "normal",
    "regulation": "gdpr"
}
```

**响应**

```json
{
    "requestId": "17284033173196154RX-223",
    "totalRecords": 3,
    "jobs": [
        {
            "jobId": "a52ca032-858e-11ef-bbb4-27391388a0a6",
            "customer": {
                "user": {
                    "key": "sampleUserKey1",
                    "action": [
                        "access"
                    ],
                    "userIDs": [
                        {
                            "namespace": "email",
                            "value": "dsmith@sample.com",
                            "type": "standard",
                            "namespaceId": 6,
                            "isDeletedClientSide": false
                        }
                    ]
                }
            }
        },
        {
            "jobId": "a52ca034-858e-11ef-bbb4-d5d952d69769",
            "customer": {
                "user": {
                    "key": "sampleUserKey2",
                    "action": [
                        "delete"
                    ],
                    "userIDs": [
                        {
                            "namespace": "email",
                            "value": "ajones@sample.com",
                            "type": "standard",
                            "namespaceId": 6,
                            "isDeletedClientSide": false
                        }
                    ]
                }
            }
        },
        {
            "jobId": "a52ca033-858e-11ef-bbb4-8361a5022341",
            "customer": {
                "user": {
                    "key": "sampleUserKey2",
                    "action": [
                        "access"
                    ],
                    "userIDs": [
                        {
                            "namespace": "email",
                            "value": "ajones@sample.com",
                            "type": "standard",
                            "namespaceId": 6,
                            "isDeletedClientSide": false
                        }
                    ]
                }
            }
        }
    ]
}
```
