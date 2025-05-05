---
title: 自定义
description: 了解如何自定义您的产品推荐。
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

# 自定义

安装产品推荐模块时，Adobe Commerce将创建`ProductRecommendationsLayout`目录。 此目录包含模板文件，您可以对其进行自定义以更改推荐在店面中的显示方式。 具体来说，您可以修改或覆盖以下模板：

`<your theme>/Magento_ProductRecommendationsLayout/web/template/recommendations.html`

有关修改模板文件的详细信息，请参阅《前端开发人员指南》中的[模板自定义](https://developer.adobe.com/commerce/frontend-core/guide/templates/walkthrough/)。

如果修改`recommendations.html`文件，则必须在文件中保留以下标记，以确保Adobe Commerce可以从店面收集推荐量度：

| 标记 | 使用 |
|---|---|
| `<div data-bind="attr : {'data-unit-id' : unitId }"...</div>` | 收集视图事件。 |
| `<a data-bind="attr : {'data-sku' : sku, 'data-unit-id'}"...</a>` | 收集点击事件。 <br/>**注意：**&#x200B;如果添加任何锚点标记，则必须包含这些属性。 |

除了`recommendations.html`文件之外，`ProductRecommendationsLayout`目录还包含以下子目录：

| 目录 | 用途 |
|---|---|
| `layout` | 包含每个页面类型的`*.xml`文件 |
| `templates` | 包含调用提取和渲染脚本的文件 |
| `web/js` | 包含为您的存储获取和渲染推荐的JavaScript文件 |
| `web/template` | 包含`magento/product-recommendations`模块的模板 |

## 推荐单元定位

当您[创建](create.md)推荐时，请指定该推荐在页面上显示的[位置](placement.md)。 推荐单元可以放置在主内容容器的顶部或底部。 但是，您可以自定义此位置。 如果创建Page Builder推荐内容类型，请使用页面生成器工具在页面上放置推荐单元。 对于所有其他页面类型，编辑创建推荐时生成的`*.xml`文件。

1. 更改为`layout`目录：

   ```bash
   cd `<your theme>/Magento_ProductRecommendationsLayout/layout`
   ```

   下表列出了此目录中存在的XML文件：

   | 文件名 | 页面 |
   |---|---|
   | `catalog_category_view.xml` | 类别 |
   | `catalog_product_view.xml` | 产品详细信息 |
   | `checkout_cart_index.xml` | 购物车 |
   | `checkout_onepage_success.xml` | 结帐 |
   | `cms_index_index.xml` | 主页 |

   >[!NOTE]
   >
   >如果您的存储使用第三方扩展，则`layout`目录中的文件名可能会不同。

1. 修改`catalog_product_view.xml`文件，使推荐单位显示在产品详细信息页面上的产品图像之后。 在自定义此XML文件之前，请查看该文件并了解需要修改的部分：

   ```xml
   <?xml version="1.0"?>
   <page xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:View/Layout/etc/page_configuration.xsd">
       <referenceBlock name="page.wrapper">
           <block class="Magento\Framework\View\Element\Template" before="-" name="product_recommendations_fetcher" template="Magento_ProductRecommendationsStorefront::fetcher.phtml" />
       </referenceBlock>
       <body>
           <referenceBlock name="main.content">
               <block class="Magento\ProductRecommendationsStorefront\Block\Renderer" after="-" name="product_recommendations_product_below_content" template="Magento_ProductRecommendationsStorefront::renderer.phtml">
                   <arguments>
                       <argument name="pagePlacement" xsi:type="string">below-main-content</argument>
                   </arguments>
               </block>
           </referenceBlock>
       </body>
   </page>
   ```

   在上述代码片段中，`main.content`引用块指示推荐单元将放置在该元素的相对位置。 其`block`元素包含`after="-"`属性，该属性指定推荐单元将显示在主内容块之后的页面上。

1. 让我们通过指定其他内容块来修改此文件。

   将引用块`name`从`main.content`更改为`product.info.media`。

   ```xml
   <?xml version="1.0"?>
   <page xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:View/Layout/etc/page_configuration.xsd">
       <referenceBlock name="page.wrapper">
           <block class="Magento\Framework\View\Element\Template" before="-" name="product_recommendations_fetcher" template="Magento_ProductRecommendationsStorefront::fetcher.phtml" />
       </referenceBlock>
       <body>
           <referenceBlock name="product.info.media">
               <block class="Magento\ProductRecommendationsStorefront\Block\Renderer" after="-" name="product_recommendations_product_below_content" template="Magento_ProductRecommendationsStorefront::renderer.phtml">
                   <arguments>
                       <argument name="pagePlacement" xsi:type="string">below-main-content</argument>
                   </arguments>
               </block>
           </referenceBlock>
       </body>
   </page>
   ```

   此更改导致推荐单位显示在产品详细信息页面上的产品图像之后。 如果希望推荐单元出现在`product.info.media`之前，请将`after="-"`属性更改为`before="-"`。 `pagePlacement`参数是不应修改的内部参数。

有关页面上块类型的详细信息，请参阅[布局概述](https://developer.adobe.com/commerce/frontend-core/guide/layouts/)。

## 自定义产品属性

开发人员通常需要访问店面推荐单位中的自定义产品属性值，以便他们可以根据这些属性为产品添加可视处理。

例如，如果您的商店销售一些有机产品，则这些产品上可能会有一个自定义属性，将其指定为`Organic = Yes`。 您可能需要在店面中访问此属性值，以便在这些产品出现在“推荐”中时为其提供特殊的可视化待遇。 同样，访问这些自定义产品属性值允许您在网站的表示层中为产品添加标记或驱动自定义逻辑。

![添加徽章](assets/unit-custom.png)

若要确保在页面上呈现推荐单元时自定义产品属性可用，请在Admin的[产品属性](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create.html?lang=zh-Hans)页面中将`Used in Product Listing`属性设置为`Yes`。

设置此属性后，JSON有效负载将包含一个包含属性代码和值的数组的`attributes`对象。 然后，您可以根据这些属性值应用自定义店面样式，例如添加特殊的可视化处理或徽章，如前所述。

>[!NOTE]
>
>产品属性更改最长可能需要一小时才能显示在JSON有效负载中。
