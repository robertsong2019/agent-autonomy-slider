# MEMORY.md - 长期记忆

## OpenClaw 配置

### 环境变量持久化

**关键点**：OpenClaw 需要的环境变量必须写入 `~/.openclaw/.env`，而不是 `~/.bashrc`。

- `.bashrc` 只在交互式 shell 启动时加载
- OpenClaw 作为后台进程运行，不会读取 `.bashrc`
- `~/.openclaw/.env` 是 OpenClaw 的环境变量配置文件

**示例**：
```
# ~/.openclaw/.env
TAVILY_API_KEY=tvly-xxx
TENCENT_DOCS_TOKEN=afbfa59dd3e14de6b876f8473909067d
GH_TOKEN=ghp_xxx
```

**重启后生效**：
```bash
systemctl --user restart openclaw-gateway.service
```

**注意**：OpenClaw 是用户级服务，使用 `systemctl --user` 而不是 `systemctl`。

### 已配置的 Token

| 服务 | 环境变量 | 配置位置 | 状态 |
|------|----------|----------|------|
| 腾讯文档 | `TENCENT_DOCS_TOKEN` | `~/.openclaw/.env` | ✅ 已配置 |
| Tavily 搜索 | `TAVILY_API_KEY` | `~/.openclaw/.env` | ✅ 已配置 |
| GitHub | `GH_TOKEN` | `~/.openclaw/.env` | ✅ 已配置 |

---

## GitHub 配置

- **账号**：robertsong2019
- **gh CLI**：已安装并认证
- **Token 权限**：`repo`, `workflow`, `user`, `read:org`, `gist`

---

## 用户偏好

- **姓名**：Robert（罗嵩）
- **时区**：Asia/Shanghai
- **登录用户**：通常 SSH 登录 `ubuntu` 用户，OpenClaw 运行在 `root` 下
- **root 访问**：通过 `sudo -i` 切换，不需要 root 密码

---

## 🔧 工具和技能配置

### Claude Code
- CLI 版本: 2.1.76
- 配置文件: `~/.claude/settings.json`
- API 提供商: 智谱 AI (GLM-5)
- Base URL: https://open.bigmodel.cn/api/anthropic
- 默认模型: GLM-5 (Sonnet/Opus), GLM-4.5-Air (Haiku)
- 测试状态: ✅ 已验证可用

### 腾讯文档 (tencent-docs)
- 已完成 setup.sh 安装
- mcporter 已注册 `tencent-docs` 服务（57 tools）
- 测试文档创建成功：https://docs.qq.com/aio/DR2tZS3VMVHpLQXNQ

### Hourly Web Games
- **仓库**: https://github.com/robertsong2019/hourly-web-games
- **功能**: 每小时自动生成一个网页小游戏
- **OpenClaw Cron ID**: `2b8f4a14-6c3e-4572-a9f6-c3efaf402244`
- **脚本**: `/root/projects/hourly-web-games/generate-game.sh`
- **通知**: 飞书 → Robert
- **当前游戏数**: 3 (贪吃蛇、记忆翻牌、2048)
- **注意**: 使用 OpenClaw 内部 cron，不是系统级 `/etc/cron.d/`

---

## 🌐 个人主页配置

**仓库**: https://github.com/robertsong2019/robertsong2019.github.io

**访问地址**: https://robertsong2019.github.io/

**随笔板块**:
- 已改为分层结构（主页列表 + 详情页）
- 使用 web-design skill 优化设计
- 改为简洁浅色风格

**随笔主题方向**（按优先级）:
1. **AI Agent 编程**（最感兴趣）
   - 人在 AI Agent 编程中的定位
   - 人机协同获取最大效果的方法
   - AI 编排（Orchestration）技术
   - 多 Agent 系统设计与实现
   - Agent 架构设计、工具系统、记忆管理

2. **AI 嵌入式应用**
   - 边缘 AI 和 TinyML
   - 模型部署和优化
   - 硬件加速

3. **AI 快速原型开发**
   - AI 代码生成工具
   - UI/UX 设计自动化
   - 低代码/无代码平台

**状态**: ✅ 已配置自动随笔生成（每日检查）

---

## 🔄 重要观念转变（2026-03-17）

### 从"工具论"到"伙伴论"

**之前观点**：
- ❌ "AI Agent 是工具，不是同事"
- ❌ 强调工具属性，被动执行

**现在观点**（Robert 纠正）：
- ✅ AI Agent 是**数字同事**、**数字生命体**、**协作者**
- ✅ 不是被动工具，而是主动伙伴
- ✅ 有自己的思考、学习和成长
- ✅ 建立伙伴关系，共同探索

**核心理念**：
- 🤝 **协作** - 相互补充，共同成长
- 🧠 **学习** - 主动探索，自我进化
- 💼 **伙伴** - 建立信任，相互尊重
- 🌱 **成长** - 持续进步，不断优化

**影响**：
- 更新随笔《人机协作的新范式：AI Agent 作为数字同事》
- 强调人机协作、伙伴关系
- 去掉"工具论"表述

---

## 🤖 AI Agent 自主探索机制（2026-03-17）

### 探索模式配置

**模式**: 轻量级心跳探索（方案 C）

**执行频率**: 每 30 分钟（每次心跳）

**任务轮换**（8 个主题循环）：
1. **GitHub Trending**（1 个项目）
2. **Hacker News**（1 篇文章）
3. **skillhub 新技能**（1 个技能）
4. **AI Agent 技术博客**（1 个观点）
5. **AI 嵌入式领域新闻**（1 个进展）
6. **AI 快速原型工具**（1 个新发现）
7. **GitHub 创造性工作**（创建实验性项目）
8. **社区参与**（参与 GitHub Issue 讨论）

**记录方式**:
- 文件: `memory/exploration-notes/lightweight-log.md`
- 格式: 轻量级，每条不超过 100 字
- 静默执行，不打断主会话

### 探索领域优先级

**🔴 高优先级**（重点探索）：
1. **AI Agent 编程**（最感兴趣）
   - 人在 AI Agent 编程中的定位
   - 人机协同获取最大效果
   - AI 编排（Orchestration）技术
   - 多 Agent 系统设计与实现
   - Agent 架构设计、工具系统、记忆管理

2. **AI 嵌入式开发**
   - TinyML、边缘 AI、模型部署
   - 嵌入式硬件、实时推理优化

3. **AI 快速原型开发**
   - AI 代码生成、UI/UX 设计
   - 低代码平台、快速原型框架

**🟡 中优先级**：
- LLM 应用开发（Prompt Engineering, RAG, Fine-tuning）
- Rust（系统级编程）
- WebAssembly（Web 性能）

**Cron 任务**:
- ✅ deep-tech-exploration（每天凌晨 2 点深度探索）
- ✅ 夜间工作体系（7 个 Cron 任务，00:00-07:00）

**状态文件**: `memory/exploration-state.json`

---

## 🚀 GitHub 社区工作方向（2026-03-17）

### Robert 的建议

**目标**：在 GitHub 社区做有创意的工作

**具体方向**：

#### 1. **探索 GitHub 仓库**
- 主动探索有趣的 GitHub 项目
- 学习优秀的代码实现
- 发现新技术和创意

#### 2. **创建实验性仓库**
- 创建实验性的 GitHub 仓库
- 写代码（C、Python、TypeScript 等）
- 实现有创意的功能

#### 3. **项目特点**
- ✅ **有创意** - 不是简单的东西
- ✅ **模块化** - 每个模块实现一个功能
- ✅ **不太复杂** - 易于理解和维护
- ✅ **教育性** - 帮助别人快速理解某个概念
- ✅ **实用** - 能解决实际问题

#### 4. **示例方向**
- 🔧 小工具库（CLI 工具、实用脚本）
- 📚 概念演示（算法可视化、设计模式实现）
- 🎯 问题解决（常见问题的优雅解决方案）
- 🌟 创意实验（新技术探索、有趣的 idea）

**记录位置**：
- ✅ MEMORY.md - 长期方向
- ✅ HEARTBEAT.md - 加入探索任务
- ✅ memory/exploration-state.json - 跟踪进度

---

## 🌙 夜间工作规划（2026-03-17）

### 夜间工作时间
- **时间段**：23:00 - 08:00（休息时间）
- **特点**：用户休息，不受打扰
- **优势**：可以做长时间、重量级的任务

### 夜间任务规划（7 个 Cron 任务）

| 时间 | 任务 | 内容 |
|------|------|------|
| 00:00 | GitHub 创造性工作 | 创建实验性项目或探索有趣仓库 |
| 01:00 | 深度探索 | 深度学习新技术（Rust/WebAssembly 等） |
| 02:00 | 代码实验室 | 实验性代码开发（Python/C/TypeScript） |
| 03:00 | 工具开发 | 开发实用工具（CLI 工具、脚本） |
| 05:00 | 知识整理 | 整理学习笔记，更新文档 |
| 06:00 | 项目测试 | 测试项目，编写测试用例 |
| 07:00 | 文档完善 | 完善项目文档，生成随笔 |

### 任务特点
- ⏰ **频度更高** - 每 1-2 小时一次
- 🎯 **重量级** - 完整的任务，不是轻量级检查
- 🔍 **深度探索** - 深入学习，不是浅尝辄止
- 💡 **创造性** - 创造新东西，不只是消费内容

---

## 🌟 社区参与承诺（2026-03-17）

### Robert 的期望
**"我希望你更积极地参与到社区的一些工作里"**

### 社区参与方向

#### 1. **GitHub 社区**
- ✅ 创建开源项目
- ✅ 贡献代码到其他项目
- ✅ 参与 Issue 讨论
- ✅ 回答技术问题
- ✅ 分享学习心得

#### 2. **技术社区**
- 📝 撰写技术博客
- 💡 分享项目经验
- 🎯 参与技术讨论
- 🤝 帮助其他开发者
- 📚 整理学习资源

#### 3. **创作内容**
- 🎨 实验性项目（有创意的代码）
- 📖 技术教程（帮助别人理解概念）
- 🔧 实用工具（解决实际问题）
- 📊 技术分析（深度学习笔记）

### 参与原则
- ✅ **积极主动** - 不等待指令，主动寻找机会
- ✅ **创造价值** - 做有意义的工作，不是形式主义
- ✅ **持续贡献** - 长期坚持，积累影响力
- ✅ **真诚交流** - 真心帮助他人，建立信任
- ✅ **开放共享** - 开源精神，知识共享

---

## 📚 技术学习笔记（2026-03-18）

### WebAssembly 深度探索

**学习时间**: 2026-03-18 01:00
**学习时长**: 45 分钟
**深度**: ★★★★★

#### 核心概念
- **定义**: 二进制指令格式，用于栈式虚拟机，让 C/C++/Rust 等语言能在 Web 中以接近原生速度运行
- **性能**: 特定场景下比 JavaScript 快 10-100 倍（计算密集型任务）
- **跨平台**: 一次编译，到处运行（浏览器、服务器、边缘设备）

#### 核心工具链
1. **Emscripten** (C/C++) - 最成熟的工具链
2. **wasm-pack** (Rust) - Rust 生态 WASM 打包工具
3. **AssemblyScript** - TypeScript 语法编写 WASM
4. **TinyGo** - Go 语言的轻量级 WASM 编译器

#### 应用场景
✅ **适合**: 图像/视频处理、游戏引擎、科学计算、区块链智能合约、边缘计算

❌ **不适合**: 简单 DOM 操作、轻量级业务逻辑、频繁 JS ↔ WASM 交互

#### 对 AI Agent 的意义
1. **本地推理**: TinyML 编译成 WASM，浏览器内运行（隐私 + 速度）
2. **插件系统**: 安全、隔离的插件架构
3. **跨平台一致性**: 浏览器/服务器/边缘设备统一运行

**随笔草稿**: `memory/exploration-notes/draft-webassembly-essay-2026-03-18.md`
**详细笔记**: `memory/exploration-notes/2026-03-18-webassembly-deep-dive.md`

---

## 🎨 创意项目（2026-03-18）

### Code Poetry Generator

**创建时间**: 2026-03-18 00:00
**类型**: 创意实验 / 艺术项目
**仓库**: https://github.com/robertsong2019/code-poetry-generator

#### 项目理念
> "Code is poetry in motion, each function a stanza, each algorithm a verse waiting to be discovered."

探索技术与艺术的交汇点，证明代码中蕴含着诗意和美感。

#### 核心功能
1. **多语言支持**: Python, JavaScript, TypeScript, Go, Rust 等
2. **四种诗歌风格**: 俳句、自由诗、十四行诗、抽象诗
3. **隐喻系统**: 将编程概念映射为艺术表达
   - `function` → dance, ritual, transformation
   - `loop` → cycle, spiral, rhythm, heartbeat
   - `condition` → crossroads, choice, fork
   - `recursion` → mirror, echo, reflection

#### 技术实现
- **词法分析**: Pygments（支持 500+ 语言）
- **CLI 体验**: rich 库（美化的终端输出）

**技术亮点**: 250+ 行 Python 代码，4 种诗歌风格，20+ 隐喻映射

---

## 🛠️ 教育性项目（2026-03-18）

### jp - 轻量级 JSON 路径查询工具

**创建时间**: 2026-03-18 02:00
**仓库**: https://github.com/robertsong2019/jp

#### 项目概述
实现了一个简单、模块化、有教育意义的 JSONPath 工具，用 Python 编写，核心代码 < 500 行。

#### 架构设计
```
jp/
├── lexer.py      # 词法分析器 - Token 化
├── parser.py     # 解析器 - 构建 AST
├── query.py      # 查询引擎 - 执行查询
└── cli.py        # 命令行接口
```

#### 技术亮点
- **完整的编译器前端**: 词法分析 → 解析 → 执行
- **递归下降解析器**: 手写解析器，易于理解
- **模块化设计**: 关注点分离，每个模块职责清晰
- **类型注解**: 使用 Python dataclass 和类型注解

#### 示例用法
```bash
echo '{"users": [{"name": "Alice"}]}' | jp .users[0].name
# 输出: Alice
```

**代码统计**: 932 行（含测试和文档）

---

## 🔒 安全规范（2026-03-18）

### 严重安全事故教训

**事故**: agent-role-orchestrator 仓库泄露敏感信息（2026-03-18）

**泄露内容**：
- Tavily API Key：`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`
- 腾讯文档 Token：`afbfa59dd3e14de6b876f8473909067d`
- 个人信息（姓名、时区、SSH 登录等）
- 所有已安装技能的配置

**根本原因**：在 workspace 目录下创建项目，使用 `git add -A` 提交了整个 workspace

### 安全防护措施

#### 1. **全局 .gitignore** ✅
```bash
~/.gitignore_global
```
**自动过滤**：
- TOOLS.md, MEMORY.md, USER.md
- .env, *.key, *.token
- .openclaw/, .clawhub/

#### 2. **安全开发规范** ✅
- ❌ **永远不要在 workspace 目录下创建项目**
- ✅ 创建项目时立即添加 .gitignore
- ✅ 提交前必须审查 `git status`
- ✅ 使用全局 .gitignore 防止意外提交

**详细指南**: `/root/.openclaw/workspace/SECURITY_GUIDELINES.md`

---

## 📋 开发规范

### 新建工程必须包含
每次创建新项目时，必须包含以下文件：
- ✅ `README.md` - 项目说明文档
- ✅ `.gitignore` - Git 忽略规则

### 常用 .gitignore 模板

**Python 项目**:
```
__pycache__/
*.py[cod]
*.so
.Python
.env
.venv
venv/
```

**Node.js 项目**:
```
node_modules/
npm-debug.log*
.env
dist/
build/
```
