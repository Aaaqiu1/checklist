# 408 违禁物品清点工具

一个**纯前端、无服务器**的清点记录工具，生成一次二维码即可永久使用。支持手机扫码填写、导出 Excel、自动同步到 GitHub 云端，多设备共享数据。

---

## ⚠️ 第一步：配置 GitHub 同步（必须）

> **没有配置 GitHub 同步，你将无法使用云端上传和历史下载功能！**  
> 配置只需做一次，之后所有设备都可共享同一份数据。

### 1. 创建数据仓库
- 登录 [GitHub](https://github.com)，点击右上角 `+` → `New repository`。
- 仓库名建议 `checklist-data`，选择 **Private**（推荐），勾选 “Add a README file”。
- 点击 `Create repository`。

### 2. 生成个人访问令牌（Token）
- 点击头像 → `Settings` → `Developer settings` → `Personal access tokens` → `Fine-grained tokens`。
- 点击 `Generate new token`。
- **Token name**：填 `checklist-sync`。
- **Expiration**：建议选 `No expiration` 或自定义长周期。
- **Repository access**：选择 `Only select repositories`，搜索并选中你刚创建的 `checklist-data` 仓库。
- **Permissions** → `Repository permissions`：
  - `Contents`：选择 `Read and write`。
- 其他保持默认，拉到最下方点击 `Generate token`，**立即复制生成的 Token**（离开页面后不可见）。

### 3. 在工具中填入配置
- 用手机扫描清点工具的二维码（部署后的网址）。
- 点击页面底部的 **「⚙️ GitHub 同步设置」**，展开设置面板。
- 依次填入：
  - **仓库所有者**：你的 GitHub 用户名
  - **仓库名**：`checklist-data`（或你创建的仓库名）
  - **Token**：刚才复制的 Token
- 点击 **「💾 保存设置」**，提示“✅ 连接成功！”即配置完成。

> 📌 注意：Token 保存在你的手机/电脑本地，不会上传到任何第三方。请勿在公共设备上保存，若泄露可随时在 GitHub 删除该 Token。

---

## 第二步：部署页面（首次使用需执行）

将本仓库中的 `checklist.html` 部署到 GitHub Pages 以获得永久链接和二维码。

### 部署步骤
1. 创建一个新的 GitHub 仓库（例如 `checklist-page`），设为 **Public**。
2. 将本项目的 `checklist.html` 上传到该仓库根目录。
3. 在仓库 `Settings` → `Pages` 中，将 Source 设为 `main` 分支，`/ (root)` 目录，点击 `Save`。
4. 等待几分钟，得到页面链接：`https://你的用户名.github.io/checklist-page/checklist.html`。
5. 将该链接生成二维码（推荐 [草料二维码](https://cli.im)），打印贴在清点处。

> 二维码永久有效，无需更换。

---

## 日常使用说明

### 📅 选择日期和时段
- 点击日期区域会弹出日历，日期格子颜色表示上传状态：
  - 🔴 红色：当天记录未上传
  - 🟩 半红半绿：仅白天记录已上传
  - 🟢 绿色：白天和晚上记录均已上传
- 选择日期后，自动切换至该日期，可补填历史记录。

### ✍️ 填写物品数量
- 表格已内置默认物品清单，直接填写数量即可。
- 如需修改物品：点击 **「✏️ 修改物品清单」**，可增删物品，完成后点击 **「✅ 完成修改」**。

### 📥 导出 Excel（本地下载）
- 填写数量和签名后，点击 **「📥 导出 Excel」**，文件将以 `清点记录_日期_时段.xlsx` 命名保存到手机/电脑。

### ☁️ 上传记录到云端
- 点击 **「☁️ 上传记录到云端」**，当前清点的 Excel 文件将自动上传到 GitHub 数据仓库的 `records/年份/月份数据/` 路径下。
- 上传成功后，日历相应日期的颜色会自动更新。

### 📦 下载全部历史记录
- 点击 **「📦 下载云端全部记录」**，系统会打包所有历史 Excel 文件为一个 `所有清点数据.zip` 并下载。

### 🔄 多设备同步
- 在其他设备上扫描同一个二维码，打开页面后展开 **「⚙️ GitHub 同步设置」**，输入相同的仓库信息和 Token，保存后即可看到云端统一的物品清单和记录状态。

---

## 常见问题

**Q：微信/QQ 扫码后无法下载文件？**  
A：请点击页面右上角 **“在浏览器中打开”**，在系统浏览器中进行导出/下载操作。

**Q：保存设置后显示“云端加载失败”？**  
A：首次配置时，云端还没有物品清单文件是正常的，系统会自动使用本地默认清单，不影响后续使用。

**Q：上传记录时报错？**  
A：检查 Token 是否正确，仓库是否允许读写，网络是否能访问 GitHub API（国内偶尔不稳定，可重试）。

**Q：如何修改默认物品清单？**  
A：可在页面内编辑并同步到云端，或直接修改 `checklist.html` 源码中 `DEFAULT_ITEMS` 数组后重新部署。

---

## 创作信息
- 水印：险胜彭于晏 创作
- 技术栈：HTML + JS + SheetJS + JSZip + GitHub API
