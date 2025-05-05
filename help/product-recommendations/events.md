---
title: 收集数据
description: 了解事件如何收集 [!DNL Product Recommendations]的数据。
feature: Services, Recommendations, Eventing
exl-id: 0d5317e3-c049-4fcd-a8e4-228668d89386
source-git-commit: 94d2a9911ab10d164d75779d1f310e5bdf2aea74
workflow-type: tm+mt
source-wordcount: '1360'
ht-degree: 0%

---

# 收集数据

当您安装和配置基于SaaS的Adobe Commerce功能（如[[!DNL Product Recommendations]](install-configure.md)或[[!DNL Live Search]](../live-search/install.md)）时，模块会将行为数据收集部署到您的店面。 此机制从购物者那里收集匿名行为数据并支持[!DNL Product Recommendations]。 例如，`view`事件用于计算`Viewed this, viewed that`推荐类型，`place-order`事件用于计算`Bought this, bought that`推荐类型。

>[!NOTE]
>
>为[!DNL Product Recommendations]目的的数据收集不包括个人身份信息(PII)。 所有用户标识符（如Cookie ID和IP地址）都经过严格匿名处理。 了解[更多](https://www.adobe.com/privacy/experience-cloud.html)。

## 医疗保健客户

如果您是医疗保健客户，并且安装了[数据服务HIPAA扩展](../data-connection/hipaa-readiness.md#installation)（它是[数据连接](../data-connection/overview.md)扩展的一部分），则不再捕获[!DNL Product Recommendations]使用的店面事件数据。 这是因为店面事件数据是在客户端生成的。 要继续捕获和发送店面事件数据，请为[!DNL Product Recommendations]重新启用事件收集。 有关详细信息，请参阅[常规配置](https://experienceleague.adobe.com/en/docs/commerce-admin/config/general/general.html#data-services)。

## 数据类型和事件

产品推荐中使用两种类型的数据：

- **行为** — 购物者在您网站上的参与数据，例如产品查看次数、添加到购物车的商品数和购买次数。
- **目录** — 产品元数据，如名称、价格、可用性等。

安装`magento/product-recommendations`模块时，Adobe Sensei会聚合行为和目录数据，并为每种推荐类型创建产品推荐。 然后，产品推荐服务以包含推荐的产品&#x200B;_项_&#x200B;的小组件的形式将这些推荐部署到您的店面。

某些推荐类型使用购物者的行为数据来训练机器学习模型，以构建个性化推荐。 其他推荐类型仅使用目录数据，不使用任何行为数据。 如果您想快速开始使用网站上的产品推荐，则可以使用以下仅目录推荐类型：

- `More like this`
- `Visual similarity`

### 冷启动

何时可以开始使用使用使用行为数据的推荐类型？ 视情况而定。 这称为&#x200B;_冷启动_&#x200B;问题。

_冷启动_&#x200B;问题是指模型训练并生效所需的时间。 对于产品推荐，这意味着在网站上部署推荐单元之前，需要等待Adobe Sensei收集足够的数据来训练其机器学习模型。 模型拥有的数据越多，推荐就越准确和有用。 由于数据收集是在实时网站上进行的，因此最好通过安装和设置`magento/production-recommendations`模块来提前启动此过程。

下表针对为每种推荐类型收集足够数据所花费的时间提供了一般性指导：

| 推荐类型 | 训练时间 | 注释 |
|---|---|---|
| 基于热门程度(`Most viewed`， `Most purchased`， `Most added to cart`) | 不同 | 取决于事件数量 — 查看次数最常见，因此学习速度更快；然后添加到购物车，再购买 |
| `Viewed this, viewed that` | 需要更多培训 | 产品查看量非常大 |
| `Viewed this, bought that`，`Bought this, bought that` | 需要最多的培训 | 购买事件是商业网站上最罕见的事件，尤其是与产品查看次数相比 |
| `Trending` | 需要三天的数据来建立热门程度基线 | 趋势是衡量产品受欢迎程度与其自身受欢迎程度基线相比的近期动向。 产品的趋势分数是使用前景集（过去24小时内的最近热门程度）和背景集（过去72小时内的热门程度基线）计算的。 如果某个项目的热门程度与其基线热门程度相比，在24小时内显着增加，则它将获得高趋势得分。 每个产品都有此分数，而任何时候得分最高的产品都包含最热门的产品集。 |

可能影响培训所需时间的其他变量：

- 更高的流量有助于更快的学习
- 某些推荐类型的训练速度比其他推荐类型快
- Adobe Commerce每四小时重新计算一次行为数据。 在您的网站上使用推荐的时间越长，推荐就越准确。

为了帮助您可视化每个推荐类型的培训进度，[创建推荐](create.md#readiness-indicators)页面会显示就绪指示器。

在实时网站上收集数据并训练机器学习模型时，您可以完成设置推荐所需的其他测试和配置任务。 当您完成此工作后，模型将有足够的数据来创建有用的推荐，从而允许您将其部署到店面。

如果您的网站没有获得大多数产品SKU的足够流量（查看次数、购买次数、趋势），则可能没有足够的数据来完成学习过程。 这会使管理员中的就绪指示器看起来卡住。 就绪指示器旨在为商家提供另一个数据点，以便选择哪种推荐类型更适合他们的商店。 这些数字可作为指引，可能永远不会达到100%。 [了解关于就绪指示器的更多信息](create.md#readiness-indicators)。

### 备用建议 {#backuprecs}

如果输入数据不足以在一个单元中提供所有请求的推荐项，Adobe Commerce将提供备用推荐以填充推荐单元。 例如，如果您将`Recommended for you`推荐类型部署到主页，则您网站上的首次购物者未生成足够的行为数据来准确推荐个性化产品。 在这种情况下，Adobe Commerce会根据`Most viewed`推荐类型向此购物者显示项目。

在输入数据收集不足的情况下，以下推荐类型回退到`Most viewed`推荐类型：

- `Recommended for you`
- `Viewed this, viewed that`
- `Viewed this, bought that`
- `Bought this, bought that`
- `Trending`
- `Conversion (view to purchase)`
- `Conversion (view to cart)`

### 活动

[Adobe Commerce店面事件收集器](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/#quick-start)列出了部署到您的店面的所有事件。 在该列表中，有一个特定于[!DNL Product Recommendations]的事件子集。 当购物者与店面上的推荐单元进行交互时，这些事件会收集数据，并有助于量度分析推荐的执行情况。

| 事件 | 描述 |
| --- | --- |
| `impression-render` | 在页面上呈现推荐单元时发送。 如果页面有两个推荐单位（已购买、已查看），则会发送两个`impression-render`事件。 此事件用于跟踪展示次数的量度。 |
| `rec-add-to-cart-click` | 购物者单击推荐单元中项目的&#x200B;**添加到购物车**&#x200B;按钮。 |
| `rec-click` | 购物者单击推荐单元中的产品。 |
| `view` | 当推荐单元变为至少50%可见（例如，通过向下滚动页面）时发送。 例如，如果推荐单元有两行，当购物者看到第二行中的一行加上一个像素时，将发送`view`事件。 如果购物者多次上下滚动页面，则发送`view`事件的次数与购物者在页面上再次看到整个推荐单元时发送的次数相同。 |

>[!NOTE]
>
>产品推荐量度已针对Luma店面进行了优化。 如果店面是通过PWA Studio实施的，请参阅[PWA文档](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/)。 如果您使用自定义前端技术，如React或Vue JS，则了解如何在Headless[&#128279;](headless.md)环境中集成产品推荐。

#### 必需的报告面板事件

需要以下事件来填充[[!DNL Product Recommendations] 仪表板](workspace.md)

| “仪表板”列 | 活动 | 加入字段 |
| ---------------- | --------- | ----------- |
| 展示次数 | `page-view`，`recs-request-sent`，`recs-response-received`，`recs-unit-render` | `unitId` |
| 视图 | `page-view`，`recs-request-sent`，`recs-response-received`，`recs-unit-render`，`recs-unit-view` | `unitId` |
| 点击次数 | `page-view`，`recs-request-sent`，`recs-response-received`，`recs-item-click`，`recs-add-to-cart-click` | `unitId` |
| 收入 | `page-view`，`recs-request-sent`，`recs-response-received`，`recs-item-click`，`recs-add-to-cart-click`，`place-order` | `unitId`，`sku`，`parentSku` |
| LT收入 | `page-view`，`recs-request-sent`，`recs-response-received`，`recs-item-click`，`recs-add-to-cart-click`，`place-order` | `unitId`，`sku`，`parentSku` |
| CTR | `page-view`，`recs-request-sent`，`recs-response-received`，`recs-unit-render`，`recs-item-click`，`recs-add-to-cart-click` | `unitId`，`sku`，`parentSku` |
| vCTR | `page-view`，`recs-request-sent`，`recs-response-received`，`recs-unit-render`，`recs-unit-view`，`recs-item-click`，`recs-add-to-cart-click` | `unitId`，`sku`，`parentSku` |

以下事件并非特定于产品推荐，而是Adobe Sensei正确解释购物者数据所必需的：

- `view`
- `add-to-cart`
- `place-order`

#### 推荐类型

此表描述了每种建议案类型使用的事件。

| 推荐类型 | 活动 | 页面 |
| --- | --- | --- |
| 查看次数最多 | `page-view`<br>`product-view` | 产品详细信息页面 |
| 购买次数最多 | `page-view`<br>`place-order` | 购物车/结帐 |
| 添加到购物车的次数最多 | `page-view`<br>`add-to-cart` | 产品详细信息页面<br>产品列表页面<br>购物车<br>愿望清单 |
| 查看了这个项目，也查看了那个项目 | `page-view`<br>`product-view` | 产品详细信息页面 |
| 查看了这个项目，购买了那个项目 | 产品推荐 | `page-view`<br>`product-view` | 产品详细信息页面<br>购物车/结帐 |
| 购买了此项，也购买了此项 | 产品推荐 | `page-view`<br>`product-view` | 产品详细信息页面 |
| 趋势 | `page-view`<br>`product-view` | 产品详细信息页面 |
| 转化：查看以购买 | 产品推荐 | `page-view`<br>`product-view` | 产品详细信息页面 |
| 转化：查看以购买 | 产品推荐 | `page-view`<br>`place-order` | 购物车/结帐 |
| 转化：查看到购物车 | 产品推荐 | `page-view`<br>`product-view` | 产品详细信息页面 |
| 转化：查看到购物车 | 产品推荐 | `page-view`<br>`add-to-cart` | 产品详细信息页面<br>产品列表页面<br>购物车<br>愿望清单 |

#### 注意事项

- 广告拦截器和隐私设置可能会阻止捕获事件，并可能导致参与和收入[量度](workspace.md#column-descriptions)少报。 此外，由于购物者离开页面或网络问题，某些事件可能无法发送。
- [Headless实施](headless.md)必须实施事件以支持“产品推荐”仪表板。
- 对于可配置产品，“产品推荐”会使用推荐单元中的父产品的图像。 如果可配置产品未指定图像，则该特定产品的推荐单元将为空。

>[!NOTE]
>
>如果启用了[Cookie限制模式](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html)，则在购物者同意使用Cookie之前，Adobe Commerce不会收集行为数据。 如果“Cookie限制模式”被禁用，Adobe Commerce会默认收集行为数据。
