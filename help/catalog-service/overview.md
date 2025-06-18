---
title: '[!DNL Catalog Service]'
description: 适用于Adobe Commerce的[!DNL Catalog Service]提供了一种检索产品显示页面和产品列表页面内容的方法，其速度比本机Adobe Commerce GraphQL查询快得多。
role: Admin, Developer
recommendations: noCatalog
exl-id: 525e3ff0-efa6-48c7-9111-d0b00f42957a
source-git-commit: ff5c717dbdd638e114bccc3f6dec26f4be269194
workflow-type: tm+mt
source-wordcount: '1095'
ht-degree: 0%

---

# Adobe Commerce的[!DNL Catalog Service]

Adobe Commerce扩展的[!DNL Catalog Service]提供丰富视图模型（只读）目录数据，以便快速而全面地呈现与产品相关的店面体验，包括：

* 产品详细信息页面
* 产品列表和类别页面
* 搜索结果页面
* 产品轮播
* 产品比较页面
* 渲染产品数据的任何其他页面，如购物车、订单和愿望清单页面

[!DNL Catalog Service]使用[GraphQL](https://graphql.org/)请求和接收目录数据，包括产品、产品属性、库存和价格。 GraphQL是一种查询语言，前端客户端使用它与在后端(如Adobe Commerce)上定义的应用程序编程接口(API)进行通信。 GraphQL是一种常用的通信方法，因为它非常轻量，允许系统集成商指定每个响应的内容和顺序。

Adobe Commerce有两个GraphQL系统。 核心GraphQL系统提供了广泛的查询（读取操作）和突变（写入操作），允许购物者与多种类型的页面交互，包括产品、客户帐户、购物车、结账等。 但是，返回产品信息的查询未针对速度进行优化。 GraphQL系统提供的服务只能对产品和相关信息进行查询。 这些查询的性能优于类似的核心查询。

目录服务可用的数据由SaaS数据导出扩展提供。 此扩展在Commerce应用程序与连接的Commerce服务之间同步数据，以确保对服务GraphQL API端点的查询返回最新的目录数据。 有关管理和排查SaaS数据导出操作问题的信息，请参阅[SaaS Data Export Guide](../data-export/overview.md)。

[!DNL Catalog Service]客户可以使用[SaaS价格索引器](../price-index/price-indexing.md)，这提供了更快的价格更新和同步时间。

## 架构

下图显示了两个GraphQL系统：

![目录体系结构图](assets/catalog-service-architecture.png)

在核心GraphQL系统中，PWA向Commerce应用程序发送请求，后者接收每个请求，对其进行处理，并可能通过多个子系统发送请求，然后向店面返回响应。 此往返可能会导致页面加载时间变慢，从而潜在地降低转化率。

[!DNL Catalog Service]是Storefront服务网关。 该服务访问一个单独的数据库，其中包含产品详细信息和相关信息，如产品属性、变型、价格和类别。 该服务通过索引保持数据库与Adobe Commerce同步。
由于服务绕过了与应用程序的直接通信，它能够减少请求的延迟和响应周期。

GraphQL的核心系统和服务不会直接相互通信。 您可以从不同的URL访问每个系统，并且调用需要不同的标头信息。 这两个GraphQL系统旨在共同使用。 [!DNL Catalog Service] GraphQL系统增强了核心系统，使产品店面体验更快。

您可以选择实施适用于Adobe Developer App Builder[&#128279;](https://developer.adobe.com/graphql-mesh-gateway/)的API Mesh，以便使用Adobe Developer将两个Adobe Commerce GraphQL系统与私有和第三方API以及其他软件接口集成。 可以配置网格以确保路由到每个端点的调用在标头中包含正确的授权信息。

## 体系结构详细信息

以下部分介绍了这两种GraphQL系统之间的一些差异。

### 架构管理

由于目录服务作为一种服务运行，因此集成商无需担心Commerce的基础版本。 所有版本的查询语法相同。 此外，该架构对于所有商家都是一致的。 这种一致性使得建立最佳实践更加容易，并显着提高了店面构件的重复使用率。

### 产品类型的简化

架构将产品类型的多样性减少为两个用例：

* 简单产品是指用单一价格和单一数量定义的产品。 目录服务将简单、虚拟、可下载和礼品卡产品类型映射到`simpleProductViews`。

* 复杂的产品由多个简单的产品组成。 元件简单产品可以有不同的价格。 也可以定义复杂产品，以便购物者可以指定简单产品的组成数量。 目录服务将可配置、捆绑包和分组的产品类型映射到`complexProductViews`。

复杂的产品选项通过其行为而非类型进行统一和区分。 每个选项值表示一个简单的产品。 此选项值可以访问简单产品属性，包括价格。 当购物者选择复杂产品的所有选项时，所选选项的组合指向特定的简单产品。 在购物者为所有可用选项选择值之前，简单产品将保持不明确。

#### 产品视图属性

简单和复杂的产品都有客户定义的属性，这些属性可显示在店面上。 这些属性作为[ProductViewAttributes](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/#productviewattribute-type)返回。 在Adobe Commerce中，可用的属性在创建产品时定义。 您可以从Adobe Commerce后端或以编程方式添加其他属性。 请参阅[扩展和自定义SaaS数据导出馈送数据](../data-export/extensibility-and-customizations.md)。

>[!TIP]
>
>您可以将[API Mesh与目录服务](mesh.md)一起使用，扩展目录服务GraphQL架构以添加数据或配置现有目录数据来启用新功能，而不是将数据类型添加到Commerce后端。

### 价格

简单产品表示具有价格的基本销售单位。 [!DNL Catalog Service]计算折扣前的常规价格以及折扣后的最终价格。 定价计算可以包括固定产品税。 它们不包括个性化促销。

复杂的产品没有确定的价格。 相反，目录服务会返回链接的单点的价格。 例如，商家最初可以为可配置产品的所有变体分配相同的价格。 如果某些尺寸或颜色不受欢迎，商家可以降低这些变体的价格。 因此，复杂（可配置）产品的价格首先显示一个价格范围，同时反映标准和不受欢迎的变体的价格。 购物者为所有可用选项选择了一个值后，店面会显示一个价格。

目录服务支持大值（最多16位）和高小数精度（最多4位小数）的价格，从而确保准确的价格更新和计算。

>[!NOTE]
>
> 拥有[!DNL Catalog Service]的Commerce客户可以使用[SaaS价格索引器](../price-index/price-indexing.md)利用其网站上更快的价格更改更新和同步时间。

## 实现

仅[!BADGE PaaS]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于云项目(Adobe管理的PaaS基础架构)和内部部署项目上的Adobe Commerce 。"}

安装程序需要配置[Commerce服务连接器](../landing/saas.md)。 完成此操作后，下一步是系统集成商更新店面代码以纳入[!DNL Catalog Service]查询。 所有[!DNL Catalog Service]查询都路由到GraphQL网关。 在新用户引导过程中提供URL。
