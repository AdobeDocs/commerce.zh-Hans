---
source-git-commit: 61e34c6fb4a004789bffa43c5b9356ad4edc685e
workflow-type: tm+mt
source-wordcount: '1182'
ht-degree: 1%

---
# 新增功能模板

## 新增功能

本页包含最近60天所做的更改。 我们将从此列表中排除所有次要更新，例如副本编辑。

### 2026年6月3日

<table style="table-layout:auto;">
  <thead>
    <tr>
      <th>描述</th>
      <th>类型</th>
      <th>Source</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><p>添加了Adobe Commerce as a Cloud Service的生产<a href="https://experienceleague.adobe.com/en/docs/commerce/cloud-service/release-notes">发行说明</a>。</p>
</td>
      <td>
        重大更新
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/8ec59cfc8c9d4d1e804adefe7f88806843e3caa3">提交</a></td>
    </tr>
    <tr>
      <td><p>为SaaS数据导出添加了<a href="https://experienceleague.adobe.com/en/docs/commerce/saas-data-export/feed-lock-mechanism">信息源锁定机制</a>，以说明信息源锁定如何防止并发同步冲突，以及如何解释Commerce数据导出日志(<code>commerce-data-export.log</code>)中包含的正常跳过消息。</p>
</td>
      <td>
        新主题
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/cb045b490482649a65bac9d763062700a90e9ecd">提交</a></td>
    </tr>
  </tbody>
</table>

### 2026年6月2日

<table style="table-layout:auto;">
  <thead>
    <tr>
      <th>描述</th>
      <th>类型</th>
      <th>Source</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><p>Commerce管理员添加了一个以资产为中心的<a href="https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/sync-status">同步状态</a>列表，用于按资产属性搜索、筛选和排除已同步的AEM Assets。</p>
</td>
      <td>
        重大更新
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/a1cb3a063d9c4595220ca431356d34e6cbe8ea33">提交</a></td>
    </tr>
  </tbody>
</table>

### 2026年6月1日

<table style="table-layout:auto;">
  <thead>
    <tr>
      <th>描述</th>
      <th>类型</th>
      <th>Source</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><p>为Adobe Commerce as a Cloud Service添加了沙盒<a href="https://experienceleague.adobe.com/en/docs/commerce/cloud-service/release-notes">发行说明</a>。</p>
</td>
      <td>
        重大更新
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/3e5f1a5366cb57cbdd1ed3f5721a82cd0c5c5271">提交</a></td>
    </tr>
  </tbody>
</table>

### 2026年5月28日

<table style="table-layout:auto;">
  <thead>
    <tr>
      <th>描述</th>
      <th>类型</th>
      <th>Source</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><ul>
  <li>改进了<a href="https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/configure-aco">为Commerce Optimizer配置AEM Assets</a>载入，因此AEM Assets设置先于租户注册，并且提供有关专用目录层和层相关限制的更明确的指导。<br /> — 更新了<a href="https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/configure-aem">为存储库访问和管道部署配置经过重新排序的安装步骤和Cloud Manager屏幕截图</a>。<br /> — 阐明了<a href="https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/setup-synchronization">配置集成</a>中基于IMS的项目ID和环境ID选择。</li>
</ul>
</td>
      <td>
        重大更新
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/de94aaad29313b3e8254d11d8801ba0d7efff3dc">提交</a></td>
    </tr>
  </tbody>
</table>

### 2026年5月22日

<table style="table-layout:auto;">
  <thead>
    <tr>
      <th>描述</th>
      <th>类型</th>
      <th>Source</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><p>添加了有关2026年5月20日版本中<a href="https://experienceleague.adobe.com/en/docs/commerce/optimizer/release-notes">Adobe Commerce Optimizer</a>和Commerce <a href="https://experienceleague.adobe.com/en/docs/commerce/optimizer/release-notes">目录服务</a>的API更新的发行说明，该版本现在在检索产品数据时强制实施记录的每个请求100-SKU限制。</p>
</td>
      <td>
        技术
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/342a3015f743e12b7089e4d430a517804a7cd40c">提交</a></td>
    </tr>
    <tr>
      <td><p>在<a href="https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-admin/rules/rules-add#intelligent-ranking-boost">添加规则</a>和<a href="https://experienceleague.adobe.com/en/docs/commerce/live-search/best-practice">最佳实践</a>中记录了[!DNL Live Search]的智能排名提升（每个规则可配置的行为权重，默认为5.0），并交叉引用了<a href="https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-admin/category-merch">类别促销</a>。 在<a href="https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking-boost">创建和管理</a>和<a href="https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/best-practice">促销规则最佳实践</a>中为[!DNL Adobe Commerce Optimizer]添加了相同的指南。</p>
</td>
      <td>
        重大更新
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/40b4528d417a4df09ac9ae9fb0d97b0f678b55ac">提交</a></td>
    </tr>
  </tbody>
</table>

### 2026年5月19日

<table style="table-layout:auto;">
  <thead>
    <tr>
      <th>描述</th>
      <th>类型</th>
      <th>Source</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><p>AEM Assets集成指南介绍了编辑器如何在<a href="https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/release-notes">AEM Assets集成v1.3.6 </a>中设置<a href="https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/configure-aem#localized-alt-text-in-aem-assets-metadata">替换文本</a>。</p>
</td>
      <td>
        重大更新
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/6d3dfbc59e72c00c3552af5805b57c69e60b38b4">提交</a></td>
    </tr>
    <tr>
      <td><p>为Adobe Commerce as a Cloud Service添加了沙盒<a href="https://experienceleague.adobe.com/en/docs/commerce/cloud-service/release-notes">发行说明</a>。</p>
</td>
      <td>
        重大更新
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/14aa082c1f0f8ce4c51328eb8ee9f4af25adf859">提交</a></td>
    </tr>
  </tbody>
</table>

### 2026年4月30日

<table style="table-layout:auto;">
  <thead>
    <tr>
      <th>描述</th>
      <th>类型</th>
      <th>Source</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><p>扩展了<a href="https://experienceleague.adobe.com/en/docs/commerce/aco-optimizer-connector/overview">Adobe Commerce Optimizer连接器概述</a>，其中包含的主要优势、端到端架构（新图表）、更清晰的范围映射、典型的设置和同步工作流、支持的方案以及先决条件或职责，因此团队可以更轻松地评估和运营集成。</p>
</td>
      <td>
        反馈、重大更新
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/fc4ac765d4bcbb8b2a0217f33b6f8a4b353e5b33">提交</a></td>
    </tr>
  </tbody>
</table>

### 2026年4月27日

<table style="table-layout:auto;">
  <thead>
    <tr>
      <th>描述</th>
      <th>类型</th>
      <th>Source</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><p>为Adobe Commerce as a Cloud Service添加了<a href="https://experienceleague.adobe.com/en/docs/commerce/cloud-service/overview">可观察性</a>页面。</p>
</td>
      <td>
        反馈，新主题
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/bf83f213d1774845c4c99f3b154e9fb3220c3cd1">提交</a></td>
    </tr>
    <tr>
      <td><p>更新了<a href="https://experienceleague.adobe.com/en/docs/commerce/app-management/manage-app/manage-app">管理您的应用程序</a>，介绍如何在“管理员”（“搜索”、“状态”和“可扩展性模式”筛选器）和“获取应用程序”路径中查找应用程序以访问Adobe Exchange，其中包含<a href="https://experienceleague.adobe.com/en/docs/commerce/app-management/overview">应用程序管理概述</a>和<a href="https://experienceleague.adobe.com/en/docs/commerce/app-management/install">安装和访问应用程序管理</a>中的链接。</p>
</td>
      <td>
        重大更新
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/780cef7af3574cd846fd7ee82d7814f2ebe9d6cc">提交</a></td>
    </tr>
    <tr>
      <td><p>添加了Adobe Commerce as a Cloud Service的生产<a href="https://experienceleague.adobe.com/en/docs/commerce/cloud-service/release-notes">发行说明</a>。</p>
</td>
      <td>
        重大更新
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/41035e75111d370e5dc40c17607337ae75f11fa0">提交</a></td>
    </tr>
  </tbody>
</table>

### 2026年4月24日

<table style="table-layout:auto;">
  <thead>
    <tr>
      <th>描述</th>
      <th>类型</th>
      <th>Source</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><p>为Adobe Commerce as a Cloud Service添加了沙盒<a href="https://experienceleague.adobe.com/en/docs/commerce/cloud-service/release-notes">发行说明</a>。</p>
</td>
      <td>
        重大更新
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/eb10bd0ff636f70360e1ca35e51b6643ad1f70d4">提交</a></td>
    </tr>
  </tbody>
</table>

### 2026年4月20日

<table style="table-layout:auto;">
  <thead>
    <tr>
      <th>描述</th>
      <th>类型</th>
      <th>Source</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><p>阐明了监视SaaS数据导出和同步的位置 — <a href="https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard">数据管理仪表板</a>、<a href="https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status">数据馈送同步状态</a>和<a href="https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/data-sync">Commerce Optimizer数据同步</a>。</p>
</td>
      <td>
        反馈，技术
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/fcb9d4ae76bf0336fbad0dbff6518ed661d5b23b">提交</a></td>
    </tr>
  </tbody>
</table>

### 2026年4月16日

<table style="table-layout:auto;">
  <thead>
    <tr>
      <th>描述</th>
      <th>类型</th>
      <th>Source</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><p>为Adobe Commerce as a Cloud Service的4月第二版生产版本更新了<a href="https://experienceleague.adobe.com/en/docs/commerce/cloud-service/release-notes#latest">发行说明</a>。</p>
</td>
      <td>
        重大更新
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/db519e8b2f21ca0185e3423a671ff5a174259834">提交</a></td>
    </tr>
  </tbody>
</table>

### 2026年4月14日

<table style="table-layout:auto;">
  <thead>
    <tr>
      <th>描述</th>
      <th>类型</th>
      <th>Source</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><p>添加了<a href="https://experienceleague.adobe.com/en/docs/commerce/optimizer/integrations-overview">[!DNL Adobe Commerce Optimizer]集成概述</a>主题，介绍每个可用的集成（Adobe Commerce Optimizer Connector、AEM Assets、AEM Sites Optimizer和Salesforce Commerce Connector）如何在Adobe Commerce Optimizer中集成，并提供指向设置和配置指南的链接。</p>
</td>
      <td>
        反馈，新主题
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/41c8bfe8f15b1988f574fe589ba6e27bb1839ba8">提交</a></td>
    </tr>
    <tr>
      <td><p>为Adobe Commerce as a Cloud Service添加了沙盒<a href="https://experienceleague.adobe.com/en/docs/commerce/cloud-service/release-notes">发行说明</a>。</p>
</td>
      <td>
        重大更新
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/8f2cc1e79ede56192a8ab03194b0f69854f89f7b">提交</a></td>
    </tr>
    <tr>
      <td><p>记录了<a href="https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/release-notes">AEM Assets集成v1.3.5</a>并更正了<a href="https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/synchronize/custom-match">自定义自动匹配</a> API请求字段(<code>eventData</code>， <code>productSku</code>)。</p>
</td>
      <td>
        新主题
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/cd7a332dd09840aabcc0efae081ba0a713506897">提交</a></td>
    </tr>
  </tbody>
</table>

### 2026年4月9日

<table style="table-layout:auto;">
  <thead>
    <tr>
      <th>描述</th>
      <th>类型</th>
      <th>Source</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><p>添加了<a href="https://experienceleague.adobe.com/en/docs/commerce/optimizer/launch/launch-checklist">启动项核对清单</a>，作为启动前验证生产[!DNL Adobe Commerce Optimizer]设置、店面上线、SEO、CDN、集成、安全性、分析和测试的参考。</p>
</td>
      <td>
        反馈，新主题
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/4846deb1c55d1df713d21c26563a288f1cb3e21b">提交</a></td>
    </tr>
  </tbody>
</table>

### 2026年4月8日

<table style="table-layout:auto;">
  <thead>
    <tr>
      <th>描述</th>
      <th>类型</th>
      <th>Source</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><p>为Adobe Commerce Optimizer添加了<a href="https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add">类别推销</a>：将类别规则与智能排名和类别页面上的手动操作结合使用。</p>
</td>
      <td>
        新主题
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/4ec91f6a761ff78e1e66ae18125296c68053b3f1">提交</a></td>
    </tr>
  </tbody>
</table>

### 2026年4月7日

<table style="table-layout:auto;">
  <thead>
    <tr>
      <th>描述</th>
      <th>类型</th>
      <th>Source</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><p>在Adobe Commerce as a Cloud Service中添加了有关<a href="https://experienceleague.adobe.com/en/docs/commerce/cloud-service/product-files">将文件添加到产品</a>的指南。</p>
</td>
      <td>
        重大更新
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/7845129c055619e09fbf7c5f860795be6bf81533">提交</a></td>
    </tr>
  </tbody>
</table>
