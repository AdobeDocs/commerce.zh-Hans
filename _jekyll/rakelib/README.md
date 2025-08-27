---
source-git-commit: 80c4b41ceb0d8809f82db61ce9c3df6b7e1d7102
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---
# Rake库文件

此目录包含按功能组织的Rake任务定义。 Rake自动加载此目录中的所有`.rake`文件。

## 文件组织

### `adobe-docs-tasks.rake`

包含Experience League上Adobe Commerce的常见要求、共享功能以及未命名任务（文档存储库Rake任务）：

- `whatsnew` — 为新闻摘要生成数据（默认：自上次更新后）
- `render` — 渲染模板化文件并维护include

### `includes.rake`

包含在`:includes`命名空间中组织的包含管理任务：

- `includes:maintain_relationships` — 发现并维护Markdown文件中的包含关系
- `includes:maintain_timestamps` — 根据包含文件更改添加/更新时间戳
- `includes:maintain_all` — 按顺序运行这两个操作
- `includes:unused` — 查找未使用的包含文件

### `images.rake`

包含在`:images`命名空间中组织的图像管理任务：

- `images:optimize` — 优化修改后未提交文件中的图像
- `images:unused` — 在项目中查找未使用的图像

## 工作原理

Rake自动发现并加载`.rake`目录中的所有`rakelib/`文件。 这允许我们：

1. **按功能组织任务** — 将与相关任务分组在一起
2. **保持主Rakefile干净** — 专注于核心项目任务
3. **轻松添加新任务组** — 只需创建新的`.rake`文件
4. **保持关注分离** — 每个文件处理特定域

## 添加新任务组

要添加一组新的相关任务，请执行以下操作：

1. 在此目录中创建新的`.rake`文件
2. 使用描述性命名空间（例如，`namespace :images`用于与图像相关的任务）
3. 在命名空间中定义您的任务
4. Rake将自动加载它们

## 示例结构

```ruby
namespace :your_namespace do
  desc 'Description of what this task does'
  task :task_name do
    # Task implementation
  end
end
```

## 使用情况

任务在创建后立即可用：

```bash
rake your_namespace:task_name
```

## 优点

- **模块性**：每个文件都侧重于特定区域
- **可维护性**：更容易查找和修改特定任务组
- **可扩展性**：可以添加多个任务组，而不会使主Rakefile混乱
- **团队开发**：不同的开发人员可以处理不同的任务组
