---
title: 自定义自动匹配
description: 了解自定义自动匹配对于具有复杂匹配逻辑或依赖第三方系统且无法将元数据填充到AEM Assets中的商户特别有用。
feature: CMS, Media, Integration
exl-id: e7d5fec0-7ec3-45d1-8be3-1beede86c87d
source-git-commit: dfc4aaf1f780eb4a57aa4b624325fa24e571017d
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# 自定义自动匹配

如果默认自动匹配策略（**OOTB自动匹配**）与您的特定业务要求不一致，请选择自定义匹配选项。 此选项支持使用[Adobe Developer App Builder](https://experienceleague.adobe.com/zh-hans/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder)开发自定义匹配器应用程序，该应用程序可处理复杂的匹配逻辑，或者处理来自无法将元数据填充到AEM Assets中的第三方系统的资源。

## 配置自定义自动匹配

1. 在Commerce管理员中，导航到&#x200B;**[!UICONTROL Store]** >配置> **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**。

1. 选择&#x200B;**[!UICONTROL Custom Matcher]**&#x200B;作为匹配规则。

1. 当您选择此匹配规则时，管理员会显示用于配置&#x200B;**端点**&#x200B;和自定义匹配逻辑所需&#x200B;**身份验证参数**&#x200B;的其他字段。

### workspace.json

**[!UICONTROL Adobe I/O Workspace Configuration]**&#x200B;字段通过导入App Builder `workspace.json`配置文件提供了一种配置自定义匹配器的简化方法。

您可以从`workspace.json`Adobe Developer Console[下载](https://developer.adobe.com/console)文件。 该文件包含App Builder工作区的所有凭据和配置详细信息。

+++示例`workspace.json`

```json
{
  "project": {
    "id": "project_id",
    "name": "project_name",
    "title": "title_name",
    "org": {
      "id": "id",
      "name": "Organization_name",
      "ims_org_id": "ims_id"
    },
    "workspace": {
      "id": "workspace_id",
      "name": "workspace_name_id",
      "title": "workspace_title_id",
      "action_url": "https://action_url.net",
      "app_url": "https://app_url.net",
      "details": {
        "credentials": [
          {
            "id": "credential_id",
            "name": "credential_name_id",
            "integration_type": "oauth_server_to_server",
            "oauth_server_to_server": {
              "client_id": "client_id",
              "client_secrets": ["secret"],
              "technical_account_email": "xx@technical_account_email.com",
              "technical_account_id": "technical_account_id",
              "scopes": [
                "AdobeID",
                "openid",
                "read_organizations",
                "additional_info.projectedProductContext",
                "additional_info.roles",
                "adobeio_api",
                "read_client_secret",
                "manage_client_secrets"
              ]
            }
          }
        ],
        "services": [
          {
            "code": "AdobeIOManagementAPISDK",
            "name": "I/O Management API"
          }
        ],
        "runtime": {
          "namespaces": [
            {
              "name": "namespace_name",
              "auth": "example_auth"
            }
          ]
        },
        "events": {
          "registrations": []
        },
        "mesh": {}
      }
    }
  }
}
```

+++

1. 将`workspace.json`文件从App Builder项目拖放到&#x200B;**[!UICONTROL Adobe I/O Workspace Configuration]**&#x200B;字段中。 或者，您可以单击浏览并选择文件。

![Workspace配置](../assets/workspace-configuration.png){width="600" zoomable="yes"}

1. 系统自动：

   * 验证JSON结构
   * 提取和填充OAuth凭据
   * 获取工作区的可用运行时操作
   * 填充&#x200B;**[!UICONTROL Product to Asset URL]**&#x200B;和&#x200B;**[!UICONTROL Asset to Product URL]**&#x200B;字段的下拉列表选项

1. 从每个流的下拉菜单中选择相应的运行时操作。

1. 单击&#x200B;**[!UICONTROL Save Config]**。

## 自定义匹配器API端点

当您使用[App Builder](https://experienceleague.adobe.com/zh-hans/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder){target=_blank}生成自定义匹配程序应用程序时，该应用程序必须公开以下端点：

* **App Builder资源到产品URL**&#x200B;端点
* **App Builder产品到资源URL**&#x200B;端点

### App Builder资源到产品URL端点

此端点检索与给定资产关联的SKU列表：

#### 使用示例

```bash
const { Core } = require('@adobe/aio-sdk')

async function main(params) {

    // Build your own matching logic here to return the products that map to the assetId
    // var productMatches = [];
    // params.assetId
    // params.eventData.assetMetadata['commerce:isCommerce']
    // params.eventData.assetMetadata['commerce:skus'][i]
    // params.eventData.assetMetadata['commerce:roles']
    // params.eventData.assetMetadata['commerce:positions'][i]
    // ...
    // End of your matching logic

    return {
        statusCode: 500,
        body: {
            asset_id: params.assetId,
            product_matches: [
                {
                    product_sku: "<YOUR-SKU-HERE>",
                    asset_roles: ["thumbnail", "image", "swatch_image", "small_image"],
                    asset_position: 1
                }
            ]
        }
    };
}

exports.main = main;
```

**请求**

```bash
POST https://your-app-builder-url/api/v1/web/app-builder-external-rule/asset-to-product
```

| 参数 | 数据类型 | 描述 |
| --- | --- | --- |
| `assetId` | 字符串 | 表示更新的资产ID。 |
| `eventData` | 字符串 | 返回与资产ID关联的数据有效负载。 |

**响应**

```bash
{
  "asset_id": "{ASSET_ID}",
  "product_matches": [
    {
      "product_sku": "{PRODUCT_SKU_1}",
      "asset_roles": ["thumbnail","image"]
    },
    {
      "product_sku": "{PRODUCT_SKU_2}",
      "asset_roles": ["thumbnail"]
    }
  ]
}
```

### App Builder产品到资源URL端点

此端点检索与给定SKU关联的资源列表：

#### 使用示例

```bash
const { Core } = require('@adobe/aio-sdk')

async function main(params) {
    // return asset matches for a product
    // Build your own matching logic here to return the assets that map to the productSku
    // var assetMatches = [];
    // params.productSku
    // ...
    // End of your matching logic

    return {
        statusCode: 500,
        body: {
            product_sku: params.productSku,
            asset_matches: [
                {
                    asset_id: "<YOUR-ASSET-ID-HERE>", // urn:aaid:aem:1aa1d5i2-17h8-40a7-a228-e3ur588deee1
                    asset_roles: ["thumbnail", "image", "swatch_image", "small_image"],
                    asset_format: "image", // can be "image" or "video"
                    asset_position: 1
                }
            ]
        }
    };
}

exports.main = main;
```

**请求**

```bash
POST https://your-app-builder-url/api/v1/web/app-builder-external-rule/product-to-asset
```

| 参数 | 数据类型 | 描述 |
| --- | --- | --- |
| `productSKU` | 字符串 | 表示更新的产品SKU。 |
| `eventData` | 字符串 | 返回与产品SKU关联的数据有效负载。 |

**响应**

```bash
{
  "product_sku": "{PRODUCT_SKU}",
  "asset_matches": [
    {
      "asset_id": "{ASSET_ID_1}",
      "asset_roles": ["thumbnail","image"],
      "asset_position": 1,
      "asset_format": image
    },
    {
      "asset_id": "{ASSET_ID_2}",
      "asset_roles": ["thumbnail"]
      "asset_position": 2,
      "asset_format": image     
    }
  ]
}
```

| 参数 | 数据类型 | 描述 |
| --- | --- | --- |
| `productSKU` | 字符串 | 表示更新的产品SKU。 |
| `asset_matches` | 字符串 | 返回与特定产品SKU关联的所有资产。 |

`asset_matches`参数包含以下属性：

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `asset_id` | 字符串 | 表示更新的资产ID。 |
| `asset_roles` | 字符串 | 返回所有可用的资源角色。 使用支持的[Commerce资源角色](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/catalog/products/digital-assets/product-image#image-roles)，如`thumbnail`、`image`、`small_image`和`swatch_image`。 |
| `asset_format` | 字符串 | 提供资源的可用格式。 可能的值为`image`和`video`。 |
| `asset_position` | 字符串 | 显示资源的位置。 |
