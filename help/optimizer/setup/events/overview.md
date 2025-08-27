---
title: 事件概述
description: 了解 [!DNL Adobe Commerce Optimizer] 用于改进搜索和推荐的事件。
role: Admin, Developer
recommendations: noCatalog
exl-id: c102c558-a680-4622-80f0-6e5c34d497e9
source-git-commit: 15a708db9a9a31798877ea3a400d5a9f6f930bda
workflow-type: tm+mt
source-wordcount: '1398'
ht-degree: 0%

---

# 活动

事件是通过利用实时数据洞察来增强购物体验并提高转化率的重要工具。

[!DNL Adobe Commerce Optimizer]自动将storefront事件部署到您的站点。 这些事件从购物者在您网站上的互动中捕获数据。 此匿名数据支持[推荐](../../manage-results/recommendation-performance.md)、[产品发现](../../manage-results/search-performance.md)和[成功量度](../../manage-results/success-metrics.md)。

>[!NOTE]
>
>数据收集不包括个人身份信息(PII)。 所有用户标识符（如Cookie ID和IP地址）都经过严格匿名处理。 [了解详情](https://www.adobe.com/privacy/experience-cloud.html)。

通过&#x200B;**事件**&#x200B;页面，您可以观察正在收集的店面事件数据。 通过查看事件数据收集，商家可以验证他们是否已正确实施店面事件，以及是否成功捕获了事件。 商家可以使用此页面识别潜在问题，并采取措施解决任何事件问题。

## 事件计数

**事件计数**&#x200B;选项卡跟踪购物者交互，如搜索、点击和购买，以帮助您分析趋势并改善购物体验。

![事件计数](../../assets/event-counts.png){zoomable="yes"}

| 字段 | 描述 |
|---|---|
| **日期范围** | 让我们指定查看特定数据子集的日期范围。 |
| 每小时&#x200B;**店面活动** | 显示店面上触发的事件数量的图形。 |
| **店面活动总数** | 可过滤的表，显示店面上触发的所有事件的详细信息。 |

## 健全性检查

**健全性检查**&#x200B;选项卡提供每个行为事件的运行状况分析，从而确保准确的数据收集和功能。&#x200B;AEM

![健全性检查](../../assets/sanity-check.png){zoomable="yes"}

| 字段 | 描述 |
|---|---|
| **日期范围** | 让我们指定查看特定数据子集的日期范围。 |
| **产品发现** | 显示个性化产品搜索结果所需的事件。 **Status**&#x200B;列指示是否已收到事件。 |
| **推荐** | 显示个性化产品推荐所需的事件。 **Status**&#x200B;列指示是否已收到事件。 |

以下部分介绍了[产品发现](#product-discovery)和[推荐](#recommendations)的事件详细信息。

### 产品发现

产品发现使用事件来增强搜索算法，例如“查看次数最多”和“查看了这个项目，查看了那个项目”。

此表描述了产品发现[排名策略](../../merchandising/rules/add.md#intelligent-ranking)使用的事件。

| 排名策略 | 活动 | 页面 |
| --- | --- | --- |
| 查看次数最多 | `page-view`<br>`product-view` | 产品详细信息页面 |
| 购买次数最多 | `page-view`<br>`place-order` | 购物车/结帐 |
| 添加到购物车的次数最多 | `page-view`<br>`add-to-cart` | 产品详细信息页面<br>产品列表页面<br>购物车<br>愿望清单 |
| 查看了这个项目，也查看了那个项目 | `page-view`<br>`product-view` | 产品详细信息页面 |

#### 必需的报告面板事件

需要一些事件来填充[搜索性能仪表板](../../manage-results/search-performance.md)

| 仪表板区域 | 活动 | 加入字段 |
| ------------------- | ------------- | ---------- |
| 独特搜索 | `page-view`，`search-request-sent`，`search-response-received` | `searchRequestId` |
| 零结果搜索 | `page-view`，`search-request-sent`，`search-response-received` | `searchRequestId` |

### Recommendations

推荐中使用了两种类型的数据：

- **行为** — 购物者在您网站上的参与数据，例如产品查看次数、添加到购物车的商品数和购买次数。
- **目录** — 产品元数据，如名称、价格、可用性等。

Adobe Sensei汇总行为和目录数据，为每个推荐类型创建推荐。 推荐服务随后以包含推荐的产品&#x200B;_项目_&#x200B;的小组件的形式将这些推荐部署到您的店面。

某些推荐类型使用购物者的行为数据来训练机器学习模型，以构建个性化推荐。 其他推荐类型仅使用目录数据，不使用任何行为数据。 如果要快速开始使用网站上的推荐，则可以使用`More like this`推荐类型。

#### 冷启动

何时可以开始使用使用使用行为数据的推荐类型？ 视情况而定。 这称为&#x200B;_冷启动_&#x200B;问题。

_冷启动_&#x200B;问题是指模型训练并生效所需的时间。 对于推荐，这意味着在网站上部署推荐单元之前，需要等待Adobe Sensei收集足够的数据来训练其机器学习模型。 模型拥有的数据越多，推荐就越准确和有用。 由于数据收集是在实时网站上进行的，因此最好提前启动此过程。

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
- [!DNL Adobe Commerce Optimizer]每四小时重新计算一次行为数据。 在您的网站上使用推荐的时间越长，推荐就越准确。

为了帮助您可视化每个推荐类型的培训进度，[创建推荐](../../merchandising/recommendations/create.md#readiness-indicators)页面会显示就绪指示器。

在实时网站上收集数据并训练机器学习模型时，您可以完成设置推荐所需的其他测试和配置任务。 当您完成此工作后，模型将有足够的数据来创建有用的推荐，从而允许您将其部署到店面。

如果您的网站没有获得大多数产品SKU的足够流量（查看次数、购买次数、趋势），则可能没有足够的数据来完成学习过程。 这可能会使推荐工作区上的就绪指示器看起来卡住。 就绪指示器旨在为商家提供另一个数据点，以便选择哪种推荐类型更适合他们的商店。 这些数字可作为指引，可能永远不会达到100%。 [了解关于就绪指示器的更多信息](../../merchandising/recommendations/create.md#readiness-indicators)。

#### 备用建议

如果输入数据不足以在一个单元中提供所有请求的推荐项，[!DNL Adobe Commerce Optimizer]将提供备份推荐以填充推荐单元。 例如，如果您将`Recommended for you`推荐类型部署到主页，则您网站上的首次购物者未生成足够的行为数据来准确推荐个性化产品。 在这种情况下，[!DNL Adobe Commerce Optimizer]根据`Most viewed`推荐类型向此购物者显示项目。

在输入数据收集不足的情况下，以下推荐类型回退到`Most viewed`推荐类型：

- `Recommended for you`
- `Viewed this, viewed that`
- `Viewed this, bought that`
- `Bought this, bought that`
- `Trending`
- `Conversion (view to purchase)`
- `Conversion (view to cart)`

#### 特定于推荐的事件

下表列出了当购物者与店面上的推荐单元进行交互时触发的事件。 收集的事件数据支持[量度](../../manage-results/recommendation-performance.md)分析推荐的执行情况。

| 事件 | 描述 |
| --- | --- |
| `impression-render` | 在页面上呈现推荐单元时发送。 如果页面有两个推荐单位（已购买、已查看），则会发送两个`impression-render`事件。 此事件用于跟踪展示次数的量度。 |
| `rec-add-to-cart-click` | 购物者单击推荐单元中项目的&#x200B;**添加到购物车**&#x200B;按钮。 |
| `rec-click` | 购物者单击推荐单元中的产品。 |
| `view` | 当推荐单元变为至少50%可见（例如，通过向下滚动页面）时发送。 例如，如果推荐单元有两行，当购物者看到第二行中的一行加上一个像素时，将发送`view`事件。 如果购物者多次上下滚动页面，则发送`view`事件的次数与购物者在页面上再次看到整个推荐单元时发送的次数相同。 |

#### 必需的报告面板事件

需要以下事件才能填充[推荐性能仪表板](../../manage-results/recommendation-performance.md)

| “仪表板”列 | 活动 | 加入字段 |
| ---------------- | --------- | ----------- |
| 展示次数 | `page-view`，`recs-request-sent`，`recs-response-received`，`recs-unit-render` | `unitId` |
| 视图 | `page-view`，`recs-request-sent`，`recs-response-received`，`recs-unit-render`，`recs-unit-view` | `unitId` |
| 点击次数 | `page-view`，`recs-request-sent`，`recs-response-received`，`recs-item-click`，`recs-add-to-cart-click` | `unitId` |
| 收入 | `page-view`，`recs-request-sent`，`recs-response-received`，`recs-item-click`，`recs-add-to-cart-click`，`place-order` | `unitId`，`sku`，`parentSku` |
| LT收入 | `page-view`，`recs-request-sent`，`recs-response-received`，`recs-item-click`，`recs-add-to-cart-click`，`place-order` | `unitId`，`sku`，`parentSku` |
| CTR | `page-view`，`recs-request-sent`，`recs-response-received`，`recs-unit-render`，`recs-item-click`，`recs-add-to-cart-click` | `unitId`，`sku`，`parentSku` |
| vCTR | `page-view`，`recs-request-sent`，`recs-response-received`，`recs-unit-render`，`recs-unit-view`，`recs-item-click`，`recs-add-to-cart-click` | `unitId`，`sku`，`parentSku` |

以下事件并非特定于推荐，而是Adobe Sensei正确解释购物者数据所必需的：

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
| 查看了这个项目，购买了那个项目 | `page-view`<br>`product-view` | 产品详细信息页面<br>购物车/结帐 |
| 购买了此项，也购买了此项 | `page-view`<br>`product-view` | 产品详细信息页面 |
| 趋势 | `page-view`<br>`product-view` | 产品详细信息页面 |
| 转化：查看以购买 | `page-view`<br>`product-view` | 产品详细信息页面 |
| 转化：查看以购买 | `page-view`<br>`place-order` | 购物车/结帐 |
| 转化：查看到购物车 | `page-view`<br>`product-view` | 产品详细信息页面 |
| 转化：查看到购物车 | `page-view`<br>`add-to-cart` | 产品详细信息页面<br>产品列表页面<br>购物车<br>愿望清单 |

## 支持

如果您发现任何数据差异，或者如果推荐和搜索结果未按预期工作，请[提交支持票证](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide)。
