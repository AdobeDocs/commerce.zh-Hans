---
title: '[!DNL Catalog Service and API Mesh]'
description: 适用于Adobe Commerce的[!DNL API Mesh]提供了一种通过公共GraphQL端点集成多个数据源的方法。
role: Admin, Developer
feature: Services, API Mesh, Catalog Service
exl-id: 903f4f96-6dba-4c45-8106-76d9845544ec
source-git-commit: 5dd290a4e10bdbd1f6c96b67ab6c9ba1598705dc
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# [!DNL Catalog Service and API Mesh]

适用于Adobe Developer App Builder[的](https://developer.adobe.com/graphql-mesh-gateway/gateway/overview/)API Mesh使开发人员能够使用Adobe I/O Runtime将私有或第三方API和其他接口与Adobe产品集成。

![目录体系结构图](assets/catalog-service-architecture-mesh.png)

要将API网格与目录服务结合使用，必须将API网格连接到您的实例，然后添加提供配置以连接到目录服务的API网格源[CommerceCatalogServiceGraph](https://github.com/adobe/api-mesh-sources/blob/main/connectors/)。

## 连接并配置API网格。

1. 按照[API Mesh Developer Guide](https://developer.adobe.com/graphql-mesh-gateway/gateway/create-mesh/)中&#x200B;_创建Mesh_&#x200B;的说明将API Mesh连接到您的Adobe Commerce实例。

   如果这是您第一次使用API Mesh，请先完成[入门流程](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic/)，然后再创建网格。

1. 使用以下格式创建一个JSON文件，如包含项目的目录服务API密钥的`variables.json`。

   ```json
   {
       "CATALOG_SERVICE_API_KEY":"your_api_key"
   }
   ```

1. 使用`CommerceCatalogServiceGraph`Adobe I/O可扩展CLI[将](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic/#install-the-aio-cli)源添加到您的网格。

   ```bash
   aio api-mesh source install "CommerceCatalogServiceGraph" -f variables.json
   ```

   `-f variables.json`选项提供更新配置所需的目录服务API密钥值。

运行此命令后，目录服务应通过API Mesh运行。 使用`aio api-mesh get`命令查看已更新网格的配置。

## API网格示例

API网格允许用户使用外部数据源来增强您的Adobe Commerce实例。 它还可用于配置现有Commerce数据以启用新功能。

### 启用层价格

在此示例中，API Mesh用于在Adobe Commerce中启用层价格。
替换`name`、`endpoint`和`x-api-key`值。

```json
{
  "meshConfig": {
    "sources": [
      {
        "name": "<Commerce Instance Name>",
        "handler": {
          "graphql": {
            "endpoint": "<Adobe Commerce GraphQL endpoint>"
          }
        },
        "transforms": [
            {
                "prefix": {
                    "includeRootOperations": true,
                    "value": "Core_"
                }
            }
        ]
      },
      {
        "name": "CommerceCatalogServiceGraph",
        "handler": {
          "graphql": {
            "endpoint": "https://commerce.adobe.io/catalog-service/graphql/",
            "operationHeaders": {
              "Magento-Store-View-Code": "{context.headers['magento-store-view-code']}",
              "Magento-Website-Code": "{context.headers['magento-website-code']}",
              "Magento-Store-Code": "{context.headers['magento-store-code']}",
              "Magento-Environment-Id": "{context.headers['magento-environment-id']}",
              "Magento-Customer-Group": "{context.headers['magento-customer-group']}"
            },
            "schemaHeaders": {
              "x-api-key": "<YOUR API-KEY>"
            }
          }
        }
      }
    ],
    "additionalTypeDefs": "extend interface ProductView {\n  price_tiers: [Core_TierPrice]\n}\n extend type SimpleProductView {\n  price_tiers: [Core_TierPrice]\n}\n extend type ComplexProductView {\n  price_tiers: [Core_TierPrice]\n}\n",
    "additionalResolvers": [
        {  
            "targetTypeName": "ProductView",
            "targetFieldName": "price_tiers",
            "sourceName": "MagentoStageCore",
            "sourceTypeName": "Query",
            "sourceFieldName": "Core_products",
            "requiredSelectionSet": "{\n    items {\n  sku\n    price_tiers {\n        quantity,\n        final_price {\n          value\n          currency\n        }\n      }\n    }\n  }",
            "sourceArgs": {
                "filter.sku.eq": "{root.sku}"
            },
            "result": "items[0].price_tiers"
        },
        {  
            "targetTypeName": "SimpleProductView",
            "targetFieldName": "price_tiers",
            "sourceName": "MagentoStageCore",
            "sourceTypeName": "Query",
            "sourceFieldName": "Core_products",
            "requiredSelectionSet": "{\n    items {\n  sku\n    price_tiers {\n        quantity,\n        final_price {\n          value\n          currency\n        }\n      }\n    }\n  }",
            "sourceArgs": {
                "filter.sku.eq": "{root.sku}"
            },
            "result": "items[0].price_tiers"
        },
        {  
            "targetTypeName": "ComplexProductView",
            "targetFieldName": "price_tiers",
            "sourceName": "MagentoStageCore",
            "sourceTypeName": "Query",
            "sourceFieldName": "Core_products",
            "requiredSelectionSet": "{\n    items {\n  sku\n    price_tiers {\n        quantity,\n        final_price {\n          value\n          currency\n        }\n      }\n    }\n  }",
            "sourceArgs": {
                "filter.sku.eq": "{root.sku}"
            },
            "result": "items[0].price_tiers"
        }
    ]
   }
}
```

配置完毕后，在Mesh中查询分层定价：

```graphql
query {
  products(skus: ["24-MB04"]) {
    sku
    description
    price_tiers {
        quantity
        final_price {
          value
          currency
        }
      }
    ... on SimpleProductView {
      id
       
      price {
        final {
          amount {
            value
          }
        }
      }
    }
  }
}
```

### 获取实体ID

此网格会将`entityId`附加到ProductView界面。 替换`name`、`endpoint`和`x-api-key`值。

```json
{
    "meshConfig": {
      "sources": [
        {
          "name": "<Commerce Instance Name>",
          "handler": {
            "graphql": {
              "endpoint": "<Adobe Commerce GraphQL endpoint>"
            }
          },
          "transforms": [
              {
                  "prefix": {
                      "includeRootOperations": true,
                        "value": "Core_"
                  }
              }
          ]
        },
        {
          "name": "CommerceCatalogServiceGraph",
          "handler": {
            "graphql": {
              "endpoint": "https://catalog-service.adobe.io/graphql",
              "operationHeaders": {
                "Magento-Store-View-Code": "{context.headers['magento-store-view-code']}",
                "Magento-Website-Code": "{context.headers['magento-website-code']}",
                "Magento-Store-Code": "{context.headers['magento-store-code']}",
                "Magento-Environment-Id": "{context.headers['magento-environment-id']}",
                "x-api-key": "<YOUR_CATALOG_SERVICE_API_KEY>",
                "Magento-Customer-Group": "{context.headers['magento-customer-group']}"
              },
              "schemaHeaders": {
                "x-api-key": "<YOUR_CATALOG_SERVICE_API_KEY>"
              }
            }
          }
        }
      ],
      "additionalTypeDefs": "extend interface ProductView {\n  entityId: String\n}\n extend type SimpleProductView {\n  entityId: String\n}\n extend type ComplexProductView {\n  entityId: String\n}\n",
      "additionalResolvers": [
        {  
            "targetTypeName": "ComplexProductView",
            "targetFieldName": "entityId",
            "sourceName": "MagentoCore",
            "sourceTypeName": "Query",
            "sourceFieldName": "Core_products",
            "requiredSelectionSet": "{ sku\n }",
            "sourceSelectionSet": "{\n    items {\n  sku\n uid\n  }\n    }",
            "sourceArgs": {
                "filter.sku.eq": "{root.sku}"
            },
            "result": "items[0].uid",
            "resultType": "String"
          },
          {
            "targetTypeName": "SimpleProductView",
            "targetFieldName": "entityId",
            "sourceName": "MagentoCore",
            "sourceTypeName": "Query",
            "sourceFieldName": "Core_products",
            "requiredSelectionSet": "{ sku\n }",
            "sourceSelectionSet": "{\n items {\n  sku\n uid\n }}",
            "sourceArgs": {
                "filter.sku.eq": "{root.sku}"
            },
            "result": "items[0].uid",
            "resultType": "String"
          }
      ]
    }
  }
```

现在可以查询`entityId`：

```graphql
query {
  products(skus: ["MH07"]){
    sku
    name
    id
    entityId
  }
}
```
