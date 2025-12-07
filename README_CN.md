# Claude Quickstarts 中文指南

Claude Quickstarts 是 Anthropic 官方维护的项目集合，旨在帮助开发者快速开始使用 Claude API 构建应用程序。每个快速入门项目都提供了一个基础框架，你可以轻松地在此基础上进行扩展和定制。

## 开始使用

要使用这些快速入门项目，你需要一个 Claude API 密钥。如果你还没有，可以在 [console.anthropic.com](https://console.anthropic.com) 免费注册。

---

## 可用的快速入门项目

### 1. 客户支持代理 (Customer Support Agent)

**路径**: `./customer-support-agent`

由 Claude 驱动的客户支持代理。这个项目展示了如何利用 Claude 的自然语言理解和生成能力，创建一个具有知识库访问能力的 AI 辅助客户支持系统。

#### 主要特性
- AI 驱动的聊天界面
- Amazon Bedrock 知识库集成（RAG 检索增强生成）
- 实时思考过程和调试信息显示
- 用户情绪检测和代理转接
- 高度可定制的 UI（使用 shadcn/ui 组件）

#### 技术栈
- Next.js 14 + React 18
- TailwindCSS + shadcn/ui
- Anthropic SDK + AI SDK
- AWS Bedrock

#### 快速开始
```bash
cd customer-support-agent
npm install
# 配置 .env.local 添加 ANTHROPIC_API_KEY
npm run dev
```

访问 http://localhost:3000

---

### 2. 财务数据分析师 (Financial Data Analyst)

**路径**: `./financial-data-analyst`

结合了 Claude 能力与交互式数据可视化的高级应用，用于通过聊天分析财务数据。

#### 主要特性
- 智能数据分析（Claude Haiku & Sonnet）
- 多格式文件上传支持（.txt, .md, .csv, .pdf, 图像）
- 丰富的图表类型：
  - 折线图（趋势分析）
  - 柱状图（对比分析）
  - 面积图（体积分析）
  - 饼图（分布分析）

#### 应用场景
- 财务报表分析
- 环境数据分析
- 体育表现追踪
- 社交媒体分析
- 健康数据监测

#### 技术栈
- Next.js 14 + React 18
- Recharts（数据可视化）
- pdfjs-dist（PDF 处理）

#### 快速开始
```bash
cd financial-data-analyst
npm install
# 配置 .env.local 添加 ANTHROPIC_API_KEY
npm run dev
```

访问 http://localhost:3000

---

### 3. 计算机使用演示 (Computer Use Demo)

**路径**: `./computer-use-demo`

展示 Claude 如何控制桌面计算机的环境和工具参考实现。支持最新的 Claude 4 系列模型。

#### 主要特性
- Docker 容器化环境
- 支持 Claude Opus 4.5、Sonnet 4.5、Haiku 4.5 等最新模型
- 完整的计算机控制工具（截图、点击、输入、编辑文件）
- 多 API 提供商支持（Anthropic、AWS Bedrock、Google Vertex AI）
- VNC 远程桌面访问

#### 可用工具
| 工具 | 功能 |
|------|------|
| `bash` | 执行 bash 命令 |
| `computer` | 屏幕截图、点击、输入、缩放 |
| `edit` | 编辑文件 |
| `run` | 运行可执行文件 |

#### 技术栈
- Python 3.11+
- Streamlit（Web UI）
- Docker

#### 快速开始
```bash
# 使用官方镜像
docker run \
    -e ANTHROPIC_API_KEY=$ANTHROPIC_API_KEY \
    -v $HOME/.anthropic:/home/computeruse/.anthropic \
    -p 5900:5900 -p 8501:8501 -p 6080:6080 -p 8080:8080 \
    -it ghcr.io/anthropics/anthropic-quickstarts:computer-use-demo-latest

# 或本地构建
cd computer-use-demo
./setup.sh
docker build . -t computer-use-demo:local
```

访问方式：
- http://localhost:8080 - 完整界面
- http://localhost:8501 - 仅 Streamlit
- http://localhost:6080/vnc.html - 仅桌面

---

### 4. 自主编码代理 (Autonomous Coding Agent)

**路径**: `./autonomous-coding`

使用 Claude Agent SDK 实现的长期运行自主编码演示。实现两代理模式，可在多个会话中构建完整应用。

#### 工作原理
1. **初始化代理**: 生成 200 个测试用例，设置项目结构，初始化 git
2. **编码代理**: 逐一实现功能，每完成一个标记为通过

#### 主要特性
- 会话持久化（通过 git 和 feature_list.json）
- 防御式安全机制
- 构建完整的 Claude.ai 克隆应用（React + Vite 前端，Express + SQLite 后端）

#### 技术栈
- Python 3.8+
- Claude Agent SDK (claude-code-sdk)
- Claude Sonnet 4.5

#### 快速开始
```bash
cd autonomous-coding
pip install -r requirements.txt

# 完整运行
python autonomous_agent_demo.py --project-dir ./my_project

# 限制迭代次数（测试用）
python autonomous_agent_demo.py --project-dir ./my_project --max-iterations 3
```

---

### 5. 代理教育实现 (Agents)

**路径**: `./agents`

使用 Claude API 的最小 LLM 代理教育实现。这不是 SDK，而是关键概念的参考实现。

#### 核心理念
> 简单基础上的复杂 AI 行为：LLM 在循环中使用工具

#### 可用工具
- 思考工具 (ThinkTool)
- 计算器 MCP 工具
- 代码执行工具
- 文件操作工具
- 网络搜索工具

#### 使用示例
```python
from agents.agent import Agent
from agents.tools.think import ThinkTool

agent = Agent(
    name="MyAgent",
    system="You are a helpful assistant.",
    tools=[ThinkTool()],
)

response = agent.run("帮我分析这个问题...")
```

---

## 项目对比

| 项目 | 主要用途 | 技术栈 | 部署方式 |
|------|--------|--------|---------|
| Customer Support | 客户支持聊天 | Next.js | Web 应用 |
| Financial Analyst | 数据分析可视化 | Next.js + Recharts | Web 应用 |
| Computer Use | 桌面自动化 | Python + Docker | 容器 |
| Autonomous Coding | AI 开发应用 | Python CLI | 命令行 |
| Agents | 代理教育 | Python 库 | 导入使用 |

---

## 环境变量配置

### JavaScript 项目
创建 `.env.local` 文件：
```bash
ANTHROPIC_API_KEY=your_api_key_here
```

### Python 项目
```bash
export ANTHROPIC_API_KEY='your_api_key_here'
```

### AWS Bedrock（如需要）
```bash
AWS_ACCESS_KEY_ID=your_access_key
AWS_SECRET_ACCESS_KEY=your_secret_key
AWS_REGION=us-west-2
```

---

## 开发命令速查

### Customer Support Agent
```bash
npm run dev          # 完整 UI
npm run dev:left     # 仅左侧栏
npm run dev:right    # 仅右侧栏
npm run dev:chat     # 仅聊天
npm run lint         # 代码检查
npm run build        # 构建
```

### Financial Data Analyst
```bash
npm run dev          # 开发服务器
npm run build        # 构建
npm run lint         # 代码检查
```

### Computer Use Demo
```bash
./setup.sh           # 设置环境
ruff check .         # 代码检查
ruff format .        # 代码格式化
pyright              # 类型检查
pytest               # 运行测试
```

---

## 更多资源

- [Claude API 文档](https://docs.claude.com)
- [Claude Cookbooks](https://github.com/anthropics/claude-cookbooks) - 常见任务的代码片段和指南
- [Claude API 基础课程](https://github.com/anthropics/courses/tree/master/anthropic_api_fundamentals)
- [Anthropic Discord 社区](https://www.anthropic.com/discord)
- [Anthropic 支持文档](https://support.anthropic.com)

---

## 贡献

欢迎为 Claude Quickstarts 仓库做出贡献！如果你有新的快速入门项目想法或现有项目的改进建议，请提交 Issue 或 Pull Request。

## 许可证

本项目采用 MIT 许可证 - 详见 [LICENSE](LICENSE) 文件。
