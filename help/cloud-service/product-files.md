---
title: 将文件添加到产品
description: 了解如何使用 [!DNL Adobe Commerce as a Cloud Service]中的文件类型产品属性将PDF、手册和数据表等文件附加到产品。
feature: Catalog Management, Products, Integration
role: Admin, Developer
level: Intermediate
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目（Adobe管理的SaaS基础架构）。"
source-git-commit: 848ba518d170c9a0270b2513fdc8efb6813f6845
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---

# 将文件添加到产品

[!DNL Adobe Commerce as a Cloud Service]支持“文件”[产品属性输入类型](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/attributes-input-types){target="_blank"}，允许商家将文件（如PDF、手册、证书和数据表）直接附加到产品。 文件存储在Amazon S3媒体存储中，可通过使用GraphQL的店面或通过REST API的集成访问。

有三种方法可以将文件上传到产品文件属性：

* [管理员UI](#upload-through-the-admin) — 在产品编辑页面上手动上传文件。
* [REST API](#upload-through-the-rest-api) — 使用S3预签名URL通过REST API上传文件。
* [产品导入](#upload-through-product-import) — 通过CSV格式提供外部URL批量导入文件。

## 先决条件

在上载文件之前，必须创建一个文件属性并将其分配给属性集。

* [创建文件属性](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create){target="_blank"} — 将&#x200B;**[!UICONTROL Catalog Input Type for Store Owner]**&#x200B;设置为&#x200B;**[!UICONTROL File]**。

* [将属性分配给属性集](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/attribute-sets#create-an-attribute-set){target="_blank"} — 将新的文件属性拖到所需的组中。

* 在[产品文件属性](https://experienceleague.adobe.com/en/docs/commerce-admin/config/catalog/product-file-attributes)配置中配置允许的文件类型和大小。

## 通过管理员上传文件

在您[创建文件属性](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create){target="_blank"}并将其分配给属性集后，可以直接从产品编辑页面上传文件。

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Catalog]** > **[!UICONTROL Products]**。

1. 打开要编辑的产品。

1. 找到文件属性字段并单击&#x200B;**[!UICONTROL Upload]**&#x200B;以选择文件。

管理员中的![上载文件按钮](./assets/upload-file.png){width="600" zoomable="yes"}

1. 单击&#x200B;**[!UICONTROL Save]**。

要替换文件，请删除现有文件并上传新文件。 上传的文件存储在Amazon S3介质存储中。

## 通过REST API上传

使用[S3预签名URL流](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/s3-uploads/){target="_blank"}以编程方式通过REST API上载文件。 此过程对产品文件属性的处理方式与对其他媒体类型（如类别图像和客户属性文件）的处理方式相同。

此过程包括四个步骤：

1. 使用文件名和`POST V1/media/initiate-upload`调用产品文件属性的`media_resource_type`。
1. 使用返回的预签名URL直接`PUT`将文件发送到Amazon S3。
1. 调用`POST V1/media/finish-upload`确认上传。
1. 通过`PUT /V1/products/{sku}`将返回的密钥分配给产品的文件属性，并将密钥作为[自定义属性](https://developer.adobe.com/commerce/webapi/rest/modules/custom-attributes/)值传递。

## 通过产品导入上传

您可以使用[导入API](https://developer.adobe.com/commerce/webapi/rest/modules/import/){target="_blank"}或管理员导入UI将文件批量附加到产品。 产品文件属性仅支持从外部URL导入，它遵循与产品图像导入[的](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/import/data-import-product-images#method-2-import-images-from-external-server){target="_blank"}方法2相同的方法。 Commerce从提供的URL下载文件，并将其保存到S3媒体存储中。

>[!NOTE]
>
>[!DNL Adobe Commerce as a Cloud Service]不支持从本地服务器路径（方法1）导入文件，因为没有直接的文件系统访问。

### 在专用列中提供URL

使用属性代码作为CSV列标题，使用完整URL作为值。 例如，如果属性代码为`file_upload`，则CSV将如下所示：

```csv
sku,name,file_upload
ADB112,"My Product",https://example.com/files/manual.pdf
```

### 在`additional_attributes`中提供URL

或者，在`additional_attributes`列中包含file属性：

```csv
sku,name,additional_attributes
ADB112,"My Product",file_upload=https://example.com/files/manual.pdf
```

在这两种情况下，URL都必须可公开访问，并且文件扩展名和大小必须符合[配置的限制](https://experienceleague.adobe.com/en/docs/commerce-admin/config/catalog/product-file-attributes){target="_blank"}。

## 通过GraphQL检索文件

在[!DNL Adobe Commerce as a Cloud Service]中，[目录服务GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/){target="_blank"}端点提供产品数据。 文件属性显示在`attributes`的`ProductView`字段中，其中`value`包含文件的完整公共URL：

```graphql
{
  products(skus: ["ADB112"]) {
    sku
    name
    attributes(roles: []) {
      name
      label
      value
    }
  }
}
```

响应包括文件属性及其公共URL：

```json
{
  "data": {
    "products": [
      {
        "sku": "ADB112",
        "name": "Example product",
        "attributes": [
          {
            "name": "file",
            "label": "FILE",
            "value": "https://<host>/media/catalog/product_file/manual.pdf",
          }
        ]
      }
    ]
  }
}
```

>[!NOTE]
>
>此查询需要`Magento-Website-Code`和`Magento-Store-View-Code`标头。 有关详细信息，请参阅[目录服务产品查询](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/){target="_blank"}。

## 通过REST API检索文件

通过[REST API](https://developer.adobe.com/commerce/webapi/reference/rest/saas/){target="_blank"} (`GET /V1/products/{sku}`)检索产品时，文件属性出现在`custom_attributes`数组中，其文件名为值：

```json
{
  "custom_attributes": [
    {
      "attribute_code": "file_upload",
      "value": "manual_7aa0b2d63f6d3dbf.pdf"
    }
  ]
}
```
