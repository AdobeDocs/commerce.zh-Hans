---
title: 设置您的店面
description: 了解如何设置 [!DNL Adobe Commerce Optimizer] 店面。
role: Developer
exl-id: 2b4c9e98-a30c-4a33-b356-556de5bd721a
source-git-commit: 134e5faeb13c37e10ccd14ae2b43f788c7d39d06
workflow-type: tm+mt
source-wordcount: '1808'
ht-degree: 0%

---

# 设置您的店面

>[!NOTE]
>
>本文档描述了早期访问开发中的产品，并未反映用于正式发布的所有功能。

本教程演示如何设置和使用[由Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/)提供支持的Adobe Commerce店面，以创建由[!DNL Adobe Commerce Optimizer]实例中的数据提供支持的高性能、可扩展且安全的Commerce店面。


## 先决条件

* 确保您拥有可以创建存储库并配置为本地开发的GitHub帐户(github.com)。

* 通过查看Commerce Storefront文档中的[概述](https://experienceleague.adobe.com/developer/commerce/storefront/get-started)，了解在Adobe Commerce Edge Delivery Services上开发Adobe Edge Storefront的概念和工作流。
* 设置开发环境


### 设置开发环境

安装在Edge Delivery Services上开发和测试[!DNL Adobe Commerce Optimizer]店面所需的Node.js和Sidekick浏览器扩展。

#### 安装节点.js

安装节点版本管理器(NVM)和所需的Node.js版本(22.13.1 LTS)。

1. 安装节点版本管理器(NVM)。

   ```bash
   curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
   ```

1. 安装Node.js和NPM。 有关详细信息，请参阅[Node.js](https://nodejs.org/en/)。

   ```bash
   nvm install 22
   ```

   ```bash
   npm install -g npm
   ```

1. 验证安装。

   ```bash
   npm -v
   ```

>[!TIP]
>
>可通过适用于Adobe Commerce[&#128279;](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder)的[App Builder和适用于Adobe Developer App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/api-mesh/getting-started-api-mesh)的API Mesh获得用于扩展和自定义[!DNL Adobe Commerce Optimizer]解决方案的其他资源。 有关访问和使用信息，请联系您的Adobe客户代表。

#### 安装Sidekick

安装Sidekick浏览器扩展以编辑、预览内容并将其发布到店面。 请参阅[Sidekick安装说明](https://www.aem.live/docs/sidekick#installation)。

## 创建您的店面

您为[!DNL Adobe Commerce Optimizer]项目创建的店面使用Edge Delivery Services店面模板上的Adobe Commerce的自定义版本。 样板是一组文件和文件夹，它们提供了店面开发的起点。 此设置过程不同于Edge Delivery Services店面[&#128279;](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/)上Adobe Commerce的标准设置过程。

>[!NOTE]
>
>本教程使用macOS、Chrome和Visual Studio Code作为开发环境。 屏幕会捕捉该设置并提供相应说明。 您可以使用不同的操作系统、浏览器和代码编辑器，但您看到的UI和执行的步骤会相应地有所不同。

### 工作流概述

按照以下步骤设置要与[!DNL Adobe Commerce Optimizer]一起使用的店面。

1. **[创建代码存储库](#step-1-create-site-code-repository)** — 从Adobe Commerce + Edge Delivery Services样板模板创建GitHub存储库。 包括来自源存储库的所有分支。
1. **[更新店面模板](#step-2-update-the-storefront-boilerplate)** — 更新`aco`分支上的自定义模板以将内容文件夹连接到店面。
1. **[部署更改](#step-3-deploy-changes)** — 使用`aco`分支中的更新代码覆盖`main`分支上的代码。
1. **[添加CodeSync应用程序](#step-5-add-the-aem-code-sync-app)** — 将您的存储库连接到Edge Delivery服务。 在完成源代码自定义并将代码推送到`main`分支之前，请勿连接代码同步应用程序。
1. **[添加内容](#step-6-add-content)** — 使用演示内容克隆工具在`https://da.live`上托管的文档创作环境中创建和初始化店面内容。
1. **[预览演示站点](#step-7-preview-demo-site)** — 连接到您的店面站点以查看[!DNL Adobe Commerce Optimizer]演示实例的示例内容和数据。
1. **[在本地环境中开发](#step-8-develop-in-your-local-environment)** — 安装所需的依赖项。 启动本地开发服务器，并更新店面配置以连接到Adobe为您配置的[!DNL Adobe Commerce Optimizer]实例。
1. **[后续步骤](#next-steps)** — 了解有关管理和显示店面中内容和数据的更多信息。


### 步骤1：创建站点代码存储库

使用Edge Delivery Services + Adobe Commerce样板模板为您的店面创建站点样板代码的GitHub存储库。

1. 登录到您的GitHub帐户。

1. 导航到[aem-boilerplate-commerce](https://github.com/hlxsites/aem-boilerplate-commerce) GitHub存储库。

1. 选择&#x200B;**使用此模板**，然后从下拉菜单中选择&#x200B;**创建新存储库**。

   ![[!DNL Create github repo from storefront boilerplate template]](./assets/storefront-create-github-repo.png){width="700" zoomable="yes"}

   此时将显示存储库配置页面。

   ![[!DNL Configure github repo to pull all branches from boilerplate repo]](./assets/storefront-configure-github-repo.png){width="700" zoomable="yes"}

1. 完成配置表单，并提供以下详细信息：

   * **存储库模板**—`hlxsites/aem-boilerplate-commerce`（默认）。
   * **包含所有分支** — 选择选项以包含所有分支。
   * **所有者** — 您的组织或帐户（必需）。
   * **存储库名称** — 新存储库的唯一名称（必需）。
   * **描述** — 存储库的简短描述（可选）。
   * **Public或Private**—Adobe建议使用public（默认）。

1. 选择&#x200B;**创建存储库**。

   几分钟后，将打开您的新存储库。

   忽略GitHub用户界面中显示的任何拉取请求通知。

### 步骤2：更新店面模板

您需要以下信息更新店面样板代码：

* 步骤2 **中的** GitHub存储库URL— `github.com/{ORG}/{SITE}`

   * `{ORG}`是存储库的组织名称或用户名

   * `{SITE}`是您的存储库名称

* 步骤1 **中的**&#x200B;内容文件夹URL— `https://drive.google.com/drive/folders/{YOUR_FOLDER_ID}`

  `{YOUR_FOLDER_ID}`是使用示例内容数据创建的文件夹的ID。

#### 将存储库链接到文档创作环境

1. 将存储库克隆到本地计算机。

   ```bash
   git clone https://github.com/{ORG}/{SITE}.git
   ```

   如果在克隆存储库时遇到错误，请参阅GitHub文档中的[克隆错误疑难解答](https://docs.github.com/en/repositories/creating-and-managing-repositories/troubleshooting-cloning-errors)。

1. 在终端或IDE中打开存储库。

1. 签出`aco`分支

   ```bash
   git checkout aco
   ```

1. 通过将`default-fstab.yaml`文件复制到`fstab.yaml`创建配置文件。

   ```bash
   cp default-fstab.yaml fstab.yaml
   ```

1. 更新店面配置文件中的挂载点以指向您的内容URL。

   1. 打开[fstab.yaml](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/#vocabulary)配置文件。

      ```yaml
      mountpoints:
        /:
          url: https://content.da.live/{org}/{site}/
          type: markup
      
      folders:
       /products/: /products/default
      ```

   1. 将`{ORG}`和`{SITE}`字符串替换为您为样板代码创建的GitHub存储库的值。

      例如，更新的代码应如下所示。

      ```yaml
      mountpoints:
        /:
          url: https://content.da.live/owner-name/aco-storefront/
          type: markup
      ```

   1. 保存文件。

#### 配置Sidekick扩展

1. 为Sidekick扩展添加项目配置。 此配置确保Sidekick可用于管理店面项目的内容。

>[!NOTE]
>
>确保已在浏览器中安装[Sidekick扩展](https://www.aem.live/docs/sidekick#installation)。

1. 打开`tools/sidekick/config.json`文件。

   +++Sidekick配置文件

   ```json
   {
     "project": "Boilerplate",
     "plugins": [
       {
         "id": "cif",
         "title": "Commerce",
         "environments": [
           "edit"
         ],
         "url": "https://main--{SITE}--{ORG}.aem.live/tools/picker/dist/index.html",
         "isPalette": true,
         "paletteRect": "top: 54px; left: 5px; bottom: 5px; width: 300px; height: calc(100% - 59px); border-radius: var(--hlx-sk-button-border-radius); overflow: hidden; resize: horizontal;"
       },
       {
         "id": "personalisation",
         "title": "Personalisation",
         "environments": [
           "edit"
         ],
         "url": "https://main--{SITE}--{ORG}.aem.live/tools/segments/dist/index.html",
         "isPalette": true,
         "paletteRect": "top: 54px; left: 5px; bottom: 5px; width: 300px; height: calc(100% - 59px); border-radius: var(--hlx-sk-button-border-radius); overflow: hidden; resize: horizontal;"
       }
     ]
   }
   ```

   有关详细信息，请参阅[Sidekick Library文档](https://www.aem.live/docs/sidekick-library)。

   +++

1. 使用GitHub存储库的值更新`url`键值。

   * 将`{ORG}`字符串替换为存储库的组织或用户名。

   * 将`{SITE}`字符串替换为存储库名称

   +++已更新配置文件的示例

   如果您的GitHub存储库名为`aco-storefront`，而您的组织为`early-adopter`，则更新的URL应如下所示：

   ```json
   {
     "project": "Boilerplate",
     "plugins": [
       {
         "id": "cif",
         "title": "Commerce",
         "environments": [
           "edit"
         ],
         "url": "https://main--aco-storefront--early-adopter.aem.live/tools/picker/dist/index.html",
         "isPalette": true,
         "paletteRect": "top: 54px; left: 5px; bottom: 5px; width: 300px; height: calc(100% - 59px); border-radius: var(--hlx-sk-button-border-radius); overflow: hidden; resize: horizontal;"
       },
       {
         "id": "personalisation",
         "title": "Personalisation",
         "environments": [
           "edit"
         ],
         "url": "https://main--aco-storefront--early-adopter.aem.live/tools/segments/dist/index.html",
         "isPalette": true,
         "paletteRect": "top: 54px; left: 5px; bottom: 5px; width: 300px; height: calc(100% - 59px); border-radius: var(--hlx-sk-button-border-radius); overflow: hidden; resize: horizontal;"
       }
     ]
   }
   ```

   +++

1. 保存文件。

### 步骤3：部署更改

若要使用自定义的店面样板代码，请用您的更新覆盖`main`分支上的代码。

1. 在编辑器或IDE中，提交并保存已更新的文件。

   ```bash
   git add .
   ```

1. 确认您正在提交两个更新的文件。

   ```bash
   git status
   On branch aco
   Your branch is up to date with 'origin/aco'.
   
   Changes to be committed:
    (use "git restore --staged <file>..." to unstage)
        new file:   fstab1.yaml
        modified:   tools/sidekick/config.json
   ```

1. 将更改提交到`aco`分支。

   ```bash
   git commit -m "Update storefront boilerplate for Adobe Commerce Optimizer"
   ```

1. 使用`aco`分支上的更改覆盖`main`分支上的样板。

   ```bash
   git push origin aco:main -f
   ```

### 步骤5：添加AEM代码同步应用程序

通过将Edge Delivery代码同步GitHub应用程序添加到存储库，将您的存储库连接到AEM服务。

>[!IMPORTANT]
>
>在将更新的样板代码上传到GitHub存储库的主分支之前，请勿连接代码同步应用程序。

1. 打开[AEM代码同步应用](https://github.com/apps/aem-code-sync)配置页面。

1. 选择&#x200B;**配置**，然后使用包含您创建的存储库的&#x200B;**组织**&#x200B;或&#x200B;**帐户**&#x200B;进行身份验证。

1. 从表单中选择&#x200B;**仅选择存储库**，然后选择您创建的存储库。

1. 选择&#x200B;**安装**&#x200B;以将AEM代码同步应用程序添加到您的存储库。

   您应该会看到一条消息，指出已成功安装应用程序。

### 步骤6：添加内容

使用站点创建器工具在`https://da.live`上托管的文档创作环境中创建和初始化店面内容。 此工具将示例内容导入文档作者环境，并完成示例内容中所有文档的内容预览和发布过程。 示例内容包括页面布局、横幅、标签和其他元素以填充您的店面。

1. 打开[站点创建者工具](https://da.live/hlxsites/aem-boilerplate-commerce/tools/site-creator/site-creator)。

1. 配置存储库：

   * 选择&#x200B;**[!UICONTROL Use Existing Repository]**。
   * 输入店面样板项目的&#x200B;**[!UICONTROL Organization/Username]**。
   * 输入&#x200B;**[!UICONTROL Repository Name]**。

1. 通过选择&#x200B;**创建站点**，导入、预览内容并将其发布到文档作者环境。

   ![[!DNL AEM demo content clone tool]](./assets/storefront-edit-initial-content.png){width="700" zoomable="yes"}

   创建站点后，您可以使用[!UICONTROL Edit content]和[!UICONTROL View Site]部分中的链接来浏览演示店面。

   指向您的内容和网站的主要链接遵循以下格式：

   * **根内容文件夹**— `https://da.live/#/{ORG}/{SITE}`
   * **站点预览**—   `https://main--{SITE}--{ORG}.aem.page/`
   * **站点生产：**— `https:/main--{SITE}--{ORG}.ae.live/`

1. 打开根内容文件夹链接以查看内容。

   ![[!DNL Storefront Document Author environment]](./assets/storefront-document-author-environment.png){width="700" zoomable="yes"}

   >[!TIP]
   >
   >在侧面导航中，使用&#x200B;[!UICONTROL **学习**]&#x200B;和&#x200B;[!UICONTROL **发现**]&#x200B;链接访问用于管理网站和网站内容的学习资源。

### 步骤7：预览演示站点

验证是否正确显示了示例内容和Adobe Commerce Optimizer演示实例中的数据。

* **示例内容**&#x200B;是从文档创作环境的内容文件夹中提供的。 它包括您网站的页面布局、横幅和标签。
* 从[!DNL Adobe Commerce Optimizer]演示实例中提供了&#x200B;**示例数据**。 数据包括产品数据，其中产品属性、图像、产品说明和价格基于店面配置文件`config.json`中指定的标题值填充。

#### 连接到您的站点以查看示例内容和数据

1. 导航到`https://main--{SITE}--{ORG}.aem.live`查看您的网站。

   将`{ORG}`和`{SITE}`替换为样板存储库的组织和名称。

   ![[!DNL ACO storefront site with boilerplate]](./assets/aco-storefront-site-boilerplate.png){width="700" zoomable="yes"}

   如果页面返回404，请验证以下内容：

   * [ `fstab.yaml`文件中的装载点指向正确的内容URL](#link-the-repository-to-the-document-author-environment)： `https://content.da.live/{ORG}/{SITE}/`
   * [您已配置代码同步应用以连接到GitHub存储库](#step-5%3A-add-the-aem-code-sync-app)。
   * [您已使用演示内容克隆工具](#step-6%3A-add-content-documents-for-your-storefront)将内容发布到文档创作环境。


1. 查看来自Commerce Optimizer默认实例的示例目录数据。

   1. 在店面标题中，单击放大镜以搜索`tires`。

      ![[!DNL View product list page]](./assets/storefront-site-with-aco-data.png){width="675" zoomable="yes"}

   1. 按&#x200B;**Enter**&#x200B;查看搜索结果页。

      ![[!DNL View search results page]](./assets/storefront-with-aco-search-results-page.png){width="675" zoomable="yes"}

      搜索结果页面组件由`search`内容文档定义。 搜索结果数据基于`config.json`中的店面配置填充。

   1. 通过选择页面上的任何轮胎产品来查看产品详细信息页面。

      ![[!DNL View product details page]](./assets/storefront-with-aco-pdp-page.png){width="675" zoomable="yes"}

      产品详细信息页面组件由`product`文件夹中的`default`内容文档定义。

### 步骤8：在本地环境中开发

在本节中，您将从本地开发环境更新店面配置。

* 更新storefront配置以连接到Adobe为您配置的[!DNL Adobe Commerce Optimizer]实例的GraphQL端点。
* 更新标头值以从实例中检索数据。

#### 启动本地开发

1. 在IDE中，签出主分支，并将其重置为远程分支上的最后一次提交。

   ```bash
   git checkout main
   git reset --hard origin/main
   ```

1. 安装所需的依赖项。

   ```bash
   npm install
   ```

1. 启动本地开发服务器。

   ```bash
   npm start
   ```

   您的样板店面的第一页应在`http://localhost:3000`处显示在您的浏览器中。

   ![[!DNL Configure github repo to pull all branches from boilerplate repo]](./assets/aco-storefront-local-dev-env.png){width="700" zoomable="yes"}


#### 更新店面配置

更新店面配置文件并在本地开发环境中预览更改。

1. 在您的IDE中，更新店面配置以连接到Adobe为您配置的[!DNL Adobe Commerce Optimizer]实例。

   1. 打开`config.json`文件。

   1. 使用[!DNL Adobe Commerce Optimizer]实例的端点更新以下值：

      * **`commerce-endpoint`** — 将现有值替换为终结点URL。

        ```json
        "commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/{tenantId}/graphql"
        ```

      * **`ac-environment-id`** — 将现有值替换为终结点URL中的租户ID。

        ```json
        "ac-environment-id": "{tenantId}"
        ```

   1. 保存文件。

      如果本地预览工作正常，则更新将应用于本地店面。

1. 检查站点以查看配置更改的结果。

   1. 在浏览器中，导航到`http://localhost:3000`并刷新页面。

   1. 在店面标题中，单击放大镜以搜索`tires`。

      ![搜索轮胎](./assets/storefront-header-empty-search-list.png){width="675" zoomable="yes"}

   1. 按&#x200B;**Enter**&#x200B;显示“搜索结果”页。

      ![标头值无效的搜索结果为空](./assets/storefront-configuration-with-incorrect-headers.png){width="675" zoomable="yes"}

      由于店面配置文件中的标头值基于默认实例，因此搜索不会返回任何结果。 现在，配置指向为您配置的[!DNL Adobe Commerce Optimizer]实例，这些值无效。

### 后续步骤

请参阅[店面和目录管理员端到端用例](./use-case/admin-use-case.md)，了解有关管理和显示店面中内容和数据的更多信息。

>[!MORELIKETHIS]
>
> 请参阅[Adobe Commerce Storefront文档](https://experienceleague.adobe.com/developer/commerce/storefront/)，了解有关更新网站内容以及与Commerce前端组件和后端数据集成的更多信息。
