---
title: 设置
description: 了解如何更改 [!DNL Product Recommendations] 数据的源以及如何启用可视化推荐。
exl-id: fe37624d-c53e-40cd-b182-10f62cba74c0
source-git-commit: c11e3fbc871600f413867e0c5c0b75ad705cf115
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# 设置

当您[为推荐配置SaaS数据空间](../landing/saas.md#saas-configuration)时，SaaS数据空间将收集目录数据和店面行为数据。 [Adobe Sensei](https://www.adobe.com/sensei.html)将分析该数据并计算用于提供产品推荐的产品关联。

用于测试或暂存的非生产环境通常不具备店面行为数据的数量或质量，因而无法提供切实可行的产品推荐。 实际购物者行为只能在生产环境中捕获。 要解决此问题，Adobe Commerce允许您将生产环境中的产品推荐与其他非生产SaaS数据空间结合使用。 通过在非生产环境中使用实际的店面数据，您可以预览购物者看到的推荐，并尝试使用不同的推荐类型和放置位置。 购物者可以预览来自不同SaaS数据空间的推荐，但不能单击该推荐。

使用暂存`environmentId`记录暂存订单。 它不会影响生产数据。 使用`alternateEnvironmentId`检索生产数据。

>[!NOTE]
>
>通过REST使用产品推荐时，`alternateEnvironmentId`参数可用于指定其他数据空间。 通过[GraphQL](https://developer.adobe.com/commerce/services/graphql/recommendations/recommendations/)使用产品推荐时，此参数不可用。

## 选择推荐源

要更改产品推荐数据的来源，请选择包含要使用的行为数据的SaaS数据空间。 在开始之前，请确保：

- 必须为您的生产环境配置[并启用](install-configure.md)店面数据收集，并[验证](verify.md)行为数据正在发送到Adobe Commerce。
- 您的非生产环境目录应该与生产目录基本相同。 使用类似的目录可确保产品推荐单元的返回与生产中的单元非常相似。

1. 登录到非生产Adobe Commerce环境的管理员。

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**营销** > _促销活动_ > **产品推荐**。

1. 单击&#x200B;**设置**。

   ![产品推荐设置](assets/settings.png)
   _设置_

1. 在&#x200B;_推荐源_&#x200B;部分中，启用&#x200B;**从其他SaaS数据空间获取推荐**&#x200B;选项。 _推荐源_&#x200B;部分仅显示在非生产环境中。

   出现&#x200B;_可用SaaS数据空间_&#x200B;的列表。

   ![产品推荐设置](assets/settings-select-saas.png)
   _设置_

1. 选择具有要使用的购物者数据的SaaS数据空间。

1. 单击&#x200B;**保存更改**。

   Adobe Commerce现在会从所选数据空间获取推荐。

   >[!NOTE]
   >
   > 虽然您可以查看从非生产店面的其他SaaS数据空间获取的推荐，但无法单击这些推荐。

### 配置新的SaaS数据空间

1. 在“推荐源”部分中，单击&#x200B;**编辑配置**。

1. 按照说明配置新的[[!DNL Commerce] 服务](/help/landing/saas.md)。

## 启用可视化推荐

如果已安装[可视化产品推荐](install-configure.md)模块，则必须启用可视化推荐才能使用[可视化相似度](type.md#visualsim)推荐类型。

在&#x200B;_可视化推荐_&#x200B;部分中，将&#x200B;**启用可视化推荐**&#x200B;设置为活动位置。
