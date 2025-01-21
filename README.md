# 微信读书笔记同步到 Notion

本项目旨在将您的微信读书笔记自动同步到 Notion，方便进行知识管理和回顾。

## 功能特性

- **自动同步**：通过 GitHub Actions，每天定时将微信读书中的划线和笔记同步至 Notion。
- **数据整合**：将微信读书的笔记、划线等信息统一存储在 Notion 数据库中，便于管理和查阅。

## 使用步骤

1. **Fork 本仓库**：点击页面右上角的 "Fork" 按钮，将此仓库复制到您的 GitHub 账户中。

2. **获取微信读书 Cookie**：
   - 在浏览器中打开 [微信读书网页版](https://weread.qq.com/)，并使用微信扫码登录。
   - 按下 `F12` 打开开发者工具，选择 "Network"（网络）选项卡。
   - 刷新页面，点击第一个请求，找到 "Headers"（标头）中的 "Cookie" 字段，复制其值。

3. **获取 Notion 集成令牌（Token）**：
   - 前往 [Notion 集成页面](https://www.notion.so/my-integrations)，点击 "New integration" 创建新集成，输入名称并提交。
   - 创建后，点击 "Show" 按钮，复制生成的令牌。

4. **获取 Notion 数据库 ID**：
   - 在 Notion 中创建一个新的数据库，或使用现有数据库。
   - 点击数据库页面右上角的 "Share" 按钮，确保已与您的集成共享。
   - 复制数据库页面的链接，例如：`https://www.notion.so/username/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx`，其中 `xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx` 即为数据库 ID。

5. **配置 GitHub Secrets**：
   - 在您的 GitHub 仓库中，点击 "Settings"（设置）> "Secrets and variables" > "Actions" > "New repository secret"。
   - 分别添加以下 Secrets：
     - `WEREAD_COOKIE`：填写步骤 2 中获取的微信读书 Cookie。
     - `NOTION_TOKEN`：填写步骤 3 中获取的 Notion 集成令牌。
     - `NOTION_DATABASE_ID`：填写步骤 4 中获取的 Notion 数据库 ID。

6. **启用 GitHub Actions**：
   - 在您的仓库中，点击 "Actions" 标签页。
   - 选择 "WeRead Sync" 工作流程，点击 "Run workflow" 手动触发一次同步，以验证配置是否正确。

## 注意事项

> [!IMPORTANT]
> 请勿在同步的 Notion 页面中添加个人笔记，每次同步会删除原有笔记并重新添加。

> [!NOTE]
> 默认情况下，GitHub Actions 每天 UTC 时间 0 点触发同步（北京时间上午 8 点）。您可以根据需要修改 `.github/workflows/weread_sync.yml` 文件中的调度时间。

## 常见问题

- **同步失败**：如果发现数据未同步，请在 GitHub Actions 中查看运行状态。红色表示失败，绿色表示成功。点击失败的任务可查看详情，检查配置是否正确。
- **属性类型错误**：如果遇到 `Categories is expected to be select` 错误，请将 Notion 模板中的 `Categories` 属性类型修改为 `Multi-select`。

## 贡献

欢迎提交问题（Issues）和合并请求（Pull Requests）来改进本项目。

## 许可证

本项目采用 MIT 许可证。详情请参阅 [LICENSE](./LICENSE) 文件。
