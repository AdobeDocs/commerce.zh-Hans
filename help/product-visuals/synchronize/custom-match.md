---
title: 自定义自动匹配
description: 了解自定义自动匹配如何特别适用于具有复杂匹配逻辑或依赖第三方系统(无法将产品可视化元数据填充到AEM Assets中)的商家。
feature: CMS, Media, Integration
source-git-commit: 3ecc429003490235211a812af064d1b10d053e38
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---


# 自定义自动匹配

如果默认自动匹配策略（**OOTB自动匹配**）与您的特定业务要求不一致，请选择自定义匹配选项。 此选项支持使用[Adobe Developer App Builder](https://experienceleague.adobe.com/zh-hans/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder)开发自定义匹配器应用程序，该应用程序可处理复杂的匹配逻辑，或来自第三方系统的资源，该第三方系统无法将产品可视化元数据填充到AEM Assets中。

## 配置自定义自动匹配

1. 在Commerce管理员中，导航到&#x200B;**[!UICONTROL Store]** >配置> **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**。

1. 选择&#x200B;**[!UICONTROL Custom Matcher]**&#x200B;作为匹配规则。

1. 当您选择此匹配规则时，管理员会显示用于配置&#x200B;**端点**&#x200B;和自定义匹配逻辑所需&#x200B;**身份验证参数**&#x200B;的其他字段。

## 自定义匹配器API端点

当您使用[App Builder](https://experienceleague.adobe.com/zh-hans/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder){target=_blank}生成自定义匹配程序应用程序时，该应用程序必须公开以下端点：

* **App Builder资源到产品URL**&#x200B;端点
* **App Builder产品到资源URL**&#x200B;端点

### App Builder资源到产品URL端点

此端点检索与给定资产关联的SKU列表：

#### 使用示例

```bash
const { Core } = require('@adobe/aio-sdk')
 
async function main (params) {
    // return the products that map to the assetId
    return {
        statusCode: 200,
        body: {
          asset_id: "urn:aaid:aem:1aa1d4a0-18b8-40a7-a228-e0ab588deee1",
          product_matches: [
            {
              product_sku: "SKU1",
              asset_roles: ["thumbnail"],
              asset_position: [1]
            }
          ]
        }
   }
}
 
exports.main = main
```

**请求**

```bash
GET https://your-app-builder-url/api/v1/web/app-builder-external-rule/asset-to-product
```

| 参数 | 数据类型 | 描述 |
| --- | --- | --- |
| `assetId` | 字符串 | 表示更新的资产ID |

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
 
async function main (params) {
    // return asset matches for a product
    return {
        statusCode: 200,
        body: {
          product_sku: params.productSku, //SKU-1
          asset_matches: [
            {
              asset_id: "urn:aaid:aem:1aa1d4a0-18b8-40a7-a228-e0ab588deee1",
              asset_roles: ["thumbnail","image"]
            }
          ]
        }
      }
}
 
exports.main = main
```

**请求**

```bash
GET https://your-app-builder-url/api/v1/web/app-builder-external-rule/product-to-asset
```

| 参数 | 数据类型 | 描述 |
| --- | --- | --- |
| `productSKU` | 字符串 | 表示更新的产品SKU |

**响应**

```bash
{
  "product_sku": "{PRODUCT_SKU}",
  "asset_matches": [
    {
      "asset_id": "{ASSET_ID_1}",
      "asset_roles": ["thumbnail","image"]
    },
    {
      "asset_id": "{ASSET_ID_2}",
      "asset_roles": ["thumbnail"]
    }
  ]
}
```

>[!TIP]
>
> 在`asset_roles`键中，使用支持的[Commerce资源角色](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/catalog/products/digital-assets/product-image#image-roles)，如`thumbnail`、`image`、`small_image`和`swatch_image`。
