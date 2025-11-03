---
title: '[!DNL Storefront Popover]'
description: ' [!DNL Live Search storefront popover] 动态返回建议的产品和缩略图。'
exl-id: 240a5333-15e9-4178-ba3c-ae6c62c2238c
source-git-commit: f96e7d8d2a31d5e0f49bd3ac2da320313908a868
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# [!DNL Storefront Popover]

当[!DNL Live Search]为[已安装](install.md)时，购物者在[!DNL popover]搜索[框中键入内容时，店面中会出现](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search.html#quick-search)。 键入每个字符后，[!DNL popover]将更新为排名最前的搜索结果的建议产品和缩略图图像。

[!DNL Live Search]返回两个或更多字符的查询结果。 对于部分匹配，每个单词的最大字符数为20。 “键入时搜索”查询中的字符数无法配置。

![[!DNL Live Search popover]](assets/storefront-search-as-you-type.png)

>[!TIP]
>
>在[设置实时搜索](workspace.md)文章中了解如何将产品属性设置为可搜索。

## [!DNL Popover]页面大小

[!DNL popover]的页面大小决定了可以返回多少行自动完成产品。 在Live Search安装过程中，`page_size`值更改为[目录搜索](https://experienceleague.adobe.com/docs/commerce-admin/config/catalog/catalog.html) - `Autocomplete Limit`设置的当前值。

默认情况下，“目录搜索 — 自动完成限制”值设置为八行。 要更改[!DNL popover]的页面大小，请执行以下操作：

1. 在&#x200B;*管理员*&#x200B;侧边栏上，转到&#x200B;**商店** >设置> **配置**。
1. 在左侧面板中，展开&#x200B;**目录**，然后从设置列表中选择&#x200B;**目录**。
1. 展开&#x200B;*目录搜索*&#x200B;部分。
1. 将&#x200B;**自动完成限制**&#x200B;设置为要在[!DNL popover]中允许的行数。
1. 完成后，单击&#x200B;**保存配置**。

## 样式[!DNL Popover]示例

您可以自定义[!DNL Popover]小部件的外观，以符合贵公司的风格和品牌指南。

[!DNL storefront popover]始终显示产品`name`和`price`，并且选择的字段不可配置。 但是，[!DNL popover]元素可以使用[CSS](https://developer.adobe.com/commerce/frontend-core/guide/css/)类设置样式。 例如，以下声明更改了[!DNL popover]容器和页脚的背景颜色。

```css
.livesearch.popover-container {
    background-color: lavender;
}

.livesearch.view-all-footer {
    background-color: magenta;
}
```

## 容器可见性

`.livesearch.popover-container`的父组件是`.search-autocomplete`。  `.active`类指示容器的可见性。 在`.active`打开时有条件地添加[!DNL popover]类。

```css
.search-autocomplete.active   /* visible */
.search-autocomplete          /* not visible */
```

有关设置店面元素样式的详细信息，请参阅[Frontend Developer Guide](https://developer.adobe.com/commerce/frontend-core/guide/css/)中的[层叠样式表(CSS)](https://developer.adobe.com/commerce/frontend-core/guide/)。

## 类选择器

您可以使用以下类选择器来设置[!DNL popover]中的容器和产品元素的样式。

- `.livesearch.popover-container`
- `.livesearch.view-all-footer`
- `.livesearch.products-container`
- `.livesearch.product-result`
- `.livesearch.product-name`
- `.livesearch.product-price`

### 容器类选择器

#### .livesearch.pover-container

![[!DNL Popover]容器](assets/livesearch-popover-container.png)

#### .livesearch.view-all-footer

![查看所有页脚](assets/livesearch-view-all-footer.png)

### 产品类选择器

#### .livesearch.products-container

![产品容器](assets/livesearch-product-container.png)

#### .livesearch.product-result

![产品结果](assets/livesearch-product-result.png)

#### .livesearch.product-name

![产品名称](assets/livesearch-product-name.png)

#### .livesearch.product-price

![产品价格](assets/livesearch-product-price.png)

#### .livesearch产品链接

![产品结果](assets/livesearch-product-link.png)

## 使用修改的主题 {#working-with-modified-theme}

您可以将[!DNL storefront popover]与自定义[主题](https://developer.adobe.com/commerce/frontend-core/guide/themes/)一起使用，该主题会继承来自&#x200B;*Luma*&#x200B;的必需文件。 不得修改`top.search`模块的`header-wrapper`中的`Magento_Search`块。

```html
<referenceContainer name="header-wrapper">
   <block class="Magento\Framework\View\Element\Template" name="top.search" as="topSearch" template="Magento_Search::form.mini.phtml">
      <arguments>
         <argument name="configProvider" xsi:type="object">Magento\Search\ViewModel\ConfigProvider</argument>
      </arguments>
   </block>
</referenceContainer>
```

## 正在禁用[!DNL popover]

要禁用[!DNL popover]并恢复标准[快速搜索](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search.html#quick-search)功能，请输入以下命令：

```bash
bin/magento module:disable Magento_LiveSearchStorefrontPopover
```

## Headless实施

对于具有Headless实施的客户，您可以使用[!DNL Live Search popover]npm包[安装](https://www.npmjs.com/package/@magento/ds-livesearch-storefront-utils)。
