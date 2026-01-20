---
title: 彩块化的类型
description: '[!DNL Live Search]个Facet是动态的，并在相关时显示在筛选器列表中。'
exl-id: cd05c0c5-1028-4d66-951d-0b61c1ecc440
source-git-commit: 458f34c45406db871ec61ff408aa624f163b6ee0
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# 彩块化的类型

[!DNL Live Search]使用各种Facet类型，只有在相关时它们才会出现在&#x200B;*筛选器*&#x200B;列表中。 可用Facet的列表会根据返回的产品而发生更改。 以下特征会影响其呈现方式和行为：

* 固定Facet — 最常用的Facet可以固定到列表顶部。 其余Facet在固定的Facet之后以&#x200B;*排序类型*&#x200B;顺序列出。
* 动态Facet - [Adobe AI](https://business.adobe.com/ai.html)发现与产品集和查询最相关的产品属性。 该计算会考虑整个目录的属性元数据，并在查询时确定与查询最相关的Facet。

  >[!NOTE]
  >
  >如果您发现在创建动态Facet后，GraphQL查询响应中会显示超时错误，请将所有Facet更改为Pinded以查看它是否解决了性能问题。

* 常用Facet — 搜索结果中最常出现的产品属性。
* 价格Facet — 按价格范围返回产品。 您可以在&#x200B;[*设置*](settings.md)&#x200B;工作区中指定选择的数量和价格范围间隔。

在查询时，[!DNL Live Search]在动态和常用Facet组中生成搜索结果。

![Facet — 价格](assets/storefront-search-results-run-price.png)

## 店面和无头选项

为[!DNL Commerce]店面呈现的Facet由搜索适配器处理，该适配器路由请求并在店面中呈现结果。 所有[!DNL Commerce]店面彩块化均使用单选选项按字母顺序排序，而不管分配给相应属性的输入类型如何。 店面中可用的Facet将根据当前主题进行渲染，并反映对分层导航的呈现所做的任何自定义设置。

相反，[headless](https://developer.adobe.com/commerce/php/architecture/technical-vision/web-api/)实现由API处理并支持其他选项。 Headless Facet可以按字母顺序或计数排序，并且可以具有单选或多选选项。

### Facet标签

对于[!DNL Commerce]店面，Facet标签由&#x200B;[*属性属性*](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create.html)确定。 对于具有多个视图的存储，可在&#x200B;*管理标签*&#x200B;下定义其他标签。 对于Headless实施，从[彩块化工作区](faceting-workspace.md)编辑标签。

### 排序类型

为店面渲染的所有Facet按字母顺序排序。 对于Headless实施，Facet可以按字母顺序或计数排序。

| 排序类型 | 描述 |
|--- |--- |
| 字母 | 在店面&#x200B;*筛选器*&#x200B;列表中，Facet按字母顺序排序。 |
| 计数 | （仅限Headless）对于Headless实施，Facet也可以按在返回的当前产品集中每个Facet找到的值数排序。 |
