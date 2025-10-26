#### **为什么需要 Obsidian MCP？**

Obsidian 是我们强大的本地知识库，但如何让它与先进的 AI 大语言模型联动，实现自动化操作呢？答案就是 Obsidian MCP (Model Communication Protocol)。通过它，我们可以将 Obsidian 从一个封闭的笔记软件，转变为一个可以被 AI 安全、精确操作的强大工具箱，实现自动化笔记创建、内容整理和命令执行。

本指南将带您一步步完成从安装到实践的全过程，使用的核心工具是 **Obsidian**、**Local REST API 插件** 以及强大的 AI 客户端 **Cherry Studio**。

---

#### **第一步：Obsidian 插件配置**

这是让外部工具能够与您的 Obsidian 仓库“对话”的基础。

1. **安装 Local REST API 插件：**
    
    - 打开 Obsidian，进入 设置 -> 第三方插件。
        
    - 关闭 安全模式。
        
    - 点击 社区插件市场 旁的 浏览 按钮。
        
    - 在搜索框中输入 Local REST API，找到并安装该插件。
        
    - 安装完成后，在插件列表中**启用**该插件。
        
2. **获取关键信息：**
    
    - 启用插件后，点击其下方的“选项”按钮，进入配置页面。
        
    - 您会看到两个重要的信息，请将它们复制或记录下来，后续会用到：
        
        - **API Key (API 密钥):** 一长串用于身份验证的字符。
            
        - **API URL (API 地址):** 插件默认会提供 HTTPS 和 HTTP 两个地址，例如 https://127.0.0.1:27124。
            

---

#### **第二步：准备运行环境 - 安装 Node.js 与 Cherry Studio**

在我们配置 Cherry Studio 之前，需要先准备好必要的运行环境。由于我们将使用 npx 命令来启动 MCP 服务器，而 npx 是 Node.js 环境的一部分，因此我们必须先确保电脑上已安装 Node.js。

**1. 安装 Node.js (npx 的运行基础)**

npx 是一个 Node.js 包执行工具，它随 Node.js 一起安装。我们的首要任务就是确保它的存在。

- **检查是否已安装：**
    
    - 打开您的命令行工具（Windows 用户请使用 **CMD** 或 **PowerShell**，macOS 用户请使用 **终端**）。
        
    - 输入命令 node -v 并按回车。
        
    - 如果屏幕上显示了版本号（如 v20.11.1），说明您已安装，可直接跳到下一步。
        
- **下载并安装 Node.js：**
    
    - 如果提示“命令未找到”，请访问 **[Node.js 官网](https://www.google.com/url?sa=E&q=https%3A%2F%2Fnodejs.org%2F)**。
        
    - 下载并安装 **LTS (长期支持)** 版本。这是最稳定、最推荐给绝大多数用户的版本。
        
    - 安装过程非常简单，保持默认选项，一路点击“下一步”即可。安装完成后，npx 命令就可以在您的系统上使用了。
        

**2. 安装 Cherry Studio (我们的 MCP 客户端)**

Cherry Studio 是一款优秀的、跨平台的 AI 聊天客户端，它原生支持 MCP 协议，并且提供了图形化的服务器配置界面，极大地简化了我们的设置流程。

- 请访问 Cherry Studio 的官方网站或 GitHub 页面，下载并安装适合您操作系统的最新版本。
---

#### **第三步：核心步骤 - 在 Cherry Studio 中创建 MCP 服务器**

这是整个流程中最关键的一步。我们将告诉 Cherry Studio 如何启动一个专门服务于 Obsidian 的 MCP 服务器。

1. **打开 MCP 配置界面：**
    
    - 启动 Cherry Studio，在左下角找到并点击 **设置 (Settings)** 图标（齿轮形状）。
        
    - 在弹出的菜单中，选择 **MCP** 选项卡。
        
2. **添加并配置 Obsidian MCP 服务器：**
    
    - 点击 Add Server 按钮，您将看到一个配置表单。
        
    - 请完全按照下图和下方的文本说明进行填写：
        
    
    (这里可以嵌入您提供的配置截图)
    
    - **名称 (Name):** Obsidian-MCP (或任何您喜欢的名字)
        
    - **类型 (Type):** 标准输入/输出 (stdio)
        
    - **命令 (Command):** npx
        
        - 解释：npx 是一个 Node.js 工具，它可以在不全局安装的情况下，直接下载并运行一个软件包。
            
    - **参数 (Parameters):**
        
		```
		-y
		@jianruidutong/obsidian-mcp
		```
        
        - 解释：我们在这里指定了要运行的 MCP 服务器软件包的名称。-y 参数是让 npx 自动确认安装。
            
    - **环境变量 (Environment Variables):**
        
        - 这是服务器的“说明书”，告诉它如何连接到您的 Obsidian。请**逐一添加**以下变量，并确保值准确无误：
            
        
	     ```
   	OBSIDIAN_API_KEY=0e92602fd05aa198ed50b5c349482148388991eeed0ca1b6fb5d8263ace384b6
		OBSIDIAN_BASE_URL=https://127.0.0.1:27124
		OBSIDIAN_VAULT_PATH=D:\Obsidian Vault\JasonOBVault1
		OBSIDIAN_VERIFY_SSL=false
		OBSIDIAN_ENABLE_CACHE=true
		```
          
        
        - **重要解释：**
            
            - OBSIDIAN_API_KEY: 粘贴您在第一步中获取的密钥。
                
            - OBSIDIAN_BASE_URL: 粘贴您获取的 API 地址。
                
            - OBSIDIAN_VAULT_PATH: 填写您 Obsidian 仓库在电脑上的**绝对路径**。
                
            - OBSIDIAN_VERIFY_SSL=false: 由于我们本地使用的是自签名 SSL 证书，需要将此项设为 false 来跳过证书验证，否则无法连接。
                
            - OBSIDIAN_ENABLE_CACHE=true: (可选) 开启缓存可以提升服务器的响应速度。
                

---

#### **第四步：启动并验证**

1. **启动服务器：**
    
    - 保存您的配置后，回到 MCP 服务器列表。
        
    - 找到您刚刚创建的 Obsidian-MCP，点击其右侧的**启动开关**。稍等片刻，开关变为蓝色或绿色，表示服务器已在后台成功运行。
        
2. **与 AI 对话：**
    
    - 回到 Cherry Studio 的主聊天界面。
        
    - 在聊天输入框的下方或旁边，找到 **工具/MCP** 按钮（通常是锤子或插件图标）。
        
    - 点击它，在弹出的列表中**勾选**或**启用** Obsidian-MCP。
        
3. **发送测试指令：**
    
    - 现在，向 AI 发送您的第一个指令：
        
        > “列出我 obsidian 中的所有笔记名称”
        

---

#### **第五步：成功！整个流程跑通**

如果一切配置正确，AI 将会调用 Obsidian-MCP 工具，访问您的本地知识库，并返回一个包含您所有笔记标题的列表。恭喜您，已经成功打通了 AI 与您个人知识大脑之间的桥梁！

---

#### **第六步：上手实践 - 常用 AI 提示词**

现在，您可以开始探索 Obsidian MCP 的强大功能了。这里提供一些即开即用的提示词，帮助您快速上手：

**1. 读取与查询 (Read & Search):**

- “请读取名为‘2025年项目规划’的笔记内容。”
    
- “搜索我的知识库中所有包含‘人工智能’和‘自动化’标签的笔记。”
    
- “帮我找到上周创建的所有关于‘周会纪要’的笔记。”
    

**2. 创建与编辑 (Create & Edit):**

- “在我的‘Inbox’文件夹下创建一个新笔记，标题是‘关于新视频的灵感’，内容是‘今天我想到一个...’。”
    
- “在我今天的日记（Daily Note）末尾追加一行内容：- 完成了 Obsidian MCP 的配置。”
    
- “将笔记‘临时想法.md’的全部内容，替换为‘这个想法已经过时了’。”