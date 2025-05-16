---
title: Adobe Commerce SaaS与PaaS的比较
description: 比较Adobe Commerce SaaS与PaaS模型，确定符合您业务需求的最佳实施方法。
role: Architect, Developer
source-git-commit: 06cd746e42bb55ce84712e9e36cd3e8aae669ed0
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 0%

---


# 功能比较

{{accs-early-access}}

Adobe Commerce提供三种部署模型：

- [Adobe Commerce as a Cloud Service](overview.md) (SaaS)
- 云端上的[Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/overview) (PaaS)
- [Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/overview)（内部部署）

此比较侧重于软件即服务(SaaS)和平台即服务(PaaS)模型之间的差异，这两个模型提供了不同级别的自定义、可扩展性和对商业实施的控制。

>[!NOTE]
>
>内部部署模型与PaaS模型具有相似的功能，因此当考虑SaaS与内部部署实施时，这种比较也适用。

## 商店管理功能

[Commerce管理UI](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/guide-overview)是访问功能的主要界面，这些功能用于管理后端商店操作、库存、定价、促销和客户交互。 但是，[!DNL Adobe Commerce as a Cloud Service]提供了独特的解决方案，这些解决方案取代了Adobe Commerce on Cloud和内部部署项目中提供的某些已知功能。

下表介绍了[!DNL Adobe Commerce as a Cloud Service]中可用的功能和替换解决方案：

<table>
    <thead>
        <tr>
            <th>PaaS模型</th>
            <th>SaaS模型</th>
            <th>详细信息</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/wysiwyg/gallery/media-gallery-asset-management">数字资产管理</a></td>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/aem-asset-management/aem-assets-integration">产品视觉效果</a></td>
            <td>一个强大的数字资产管理(DAM)系统，与Adobe Experience Manager集成以管理富媒体内容。 或者，默认的数字文件和资产管理功能提供了用于存储和管理数字资产的基本资产管理工具。</td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/guide-overview">内容管理系统(CMS)</a></td>
            <td rowspan="3"><a href="https://experienceleague.adobe.com/developer/commerce/storefront/merchants/get-started/">店面建置器</a></td>
            <td rowspan="3">CMS允许用户使用文档创作或可视编辑器轻松创建和管理店面内容，并包括本机实验功能。</td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/page-builder/guide-overview">页面生成器</a></td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/seo/url-rewrites/url-rewrite">URL重写</a></td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/staging/content-staging">内容暂存</a></td>
            <td rowspan="2"><a href="../catalog-service/overview.md">目录服务</a></td>
            <td rowspan="2">一种丰富的视图模型（只读）服务，用于管理目录数据和呈现与产品相关的店面体验。</td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/merchandising/visual-merch/visual-merchandiser">Visual Merchandiser</a></td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/payments/payments">支付</a></td>
            <td><a href="../payment-services/guide-overview.md">支付服务</a></td>
            <td>有助于安全高效地进行交易的集成支付服务。</td>
        </tr>
    </tbody>
</table>

## 可扩展性和平台功能

下表比较了平台功能和可扩展性特征，以帮助您了解这些差异，并在开始实施之前就哪种模式最符合您的业务需求做出明智的决策。

<table>
    <thead>
        <tr>
            <th>功能</th>
            <th>SaaS模型</th>
            <th>PaaS模型</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>平台功能</strong></td>
        </tr>
        <tr>
            <td>B2B功能</td>
            <td>预安装了核心B2B功能<sup>1</sup></td>
            <td>安装后提供完整的B2B功能</td>
        </tr>
        <tr>
            <td>试验</td>
            <td>A/B测试可优化参与和转化</td>
            <td>用于特定层的附加组件</td>
        </tr>
        <tr>
            <td>功能和安全更新</td>
            <td>自动部署</td>
            <td>需要手动升级和修补</td>
        </tr>
        <tr>
            <td>托管基础结构</td>
            <td>多租户</td>
            <td>单租户</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Commerce管理员自定义</strong></td>
        </tr>
        <tr>
            <td>可扩展的核心管理屏幕</td>
            <td>预设滤镜、可见性控件</td>
            <td>完整的布局和功能自定义</td>
        </tr>
        <tr>
            <td>可扩展的新管理屏幕</td>
            <td>外部应用程序注入(管理员UI SDK)</td>
            <td>标准管理员UI集成和外部应用程序注入(管理员UI SDK)</td>
        </tr>
        <tr>
            <td>可自定义的管理员主题</td>
            <td>无主题框架</td>
            <td>可扩展主题框架</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>可扩展性</strong></td>
        </tr>
        <tr>
            <td>可扩展性模型</td>
            <td>仅限进程外(API、事件、App Builder)</td>
            <td>进程内（PHP自定义）和进程外(API、事件、App Builder)</td>
        </tr>
        <tr>
            <td>可扩展的Web API</td>
            <td>带有自定义解析器的API网格</td>
            <td>本机REST/GraphQL可扩展性和带有自定义解析器的API网格</td>
        </tr>
        <tr>
            <td>数据模型可扩展性</td>
            <td>核心和B2B实体的自定义属性<sup>2</sup></td>
            <td>完成数据模型自定义</td>
        </tr>
        <tr>
            <td>技术</td>
            <td>CSS、CLI、HTML、JS、节点</td>
            <td>CSS、CLI、HTML、JS、PHP、XML</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>数据和存储</strong></td>
        </tr>
        <tr>
            <td>搜索索引自定义</td>
            <td>需要第三方解决方案</td>
            <td>本机搜索自定义</td>
        </tr>
        <tr>
            <td>自定义电子邮件类型</td>
            <td>仅限标准电子邮件模板</td>
            <td>完整的电子邮件自定义</td>
        </tr>
        <tr>
            <td>自定义数据存储</td>
            <td>App Builder状态库（仅限文件）<sup>3</sup></td>
            <td>数据库、文件、缓存、队列</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td colspan="3">
                <sup>1</sup>核心<a href="https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/guide-overview">B2B功能</a>（如公司管理和报价）在SaaS中现成可用。 但是，特定于行业的自定义可能需要其他实施注意事项。
                <br><br>
                SaaS中的<sup>2</sup>数据模型可扩展性支持<a href="https://developer.adobe.com/commerce/services/cloud/guides/custom-attributes/">扩展核心实体</a>超出产品和客户范围，包括B2B实体。 但是，行业特定的数据模型（例如，经销商特定的属性）可能需要额外的体系结构考虑。
                <br><br>
                <sup>3</sup> Adobe正在积极工作Document DB集成，以满足SaaS的永久存储需求。 目前，需要长期数据存储的实施可能需要调配和维护额外的基础架构。
            </td>
        </tr>
    </tfoot>
</table>

>[!NOTE]
>
>在考虑迁移到SaaS时，Adobe建议您：
>
>- 尽可能将适当的功能移到进程外可扩展性。
>- 减小需要过渡的曲面面积。
>- 请考虑使用API Mesh来扩展API功能。
>- 监控Adobe的持续平台演变和新功能发布。
>- 根据可用的可扩展性选项评估特定于行业的数据模型要求。
>- 考虑采用由渠道和策略提供支持的[促销服务](../optimizer/catalog/overview.md)。

