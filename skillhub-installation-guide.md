# skillhub 安装指南

## 📦 简介

skillhub 是一个 AI Agent 技能仓库 CLI 工具，用于搜索、安装和管理 Agent 技能。

**特点**：
- 🇨🇳 国内优化源，访问速度快
- 🔍 搜索和发现技能
- 📦 一键安装技能
- 🔄 升级已安装技能
- 📋 列出本地技能

---

## ✅ 检查是否已安装

```bash
which skillhub
```

如果输出路径（如 `/root/.local/bin/skillhub`），说明已安装。

查看版本：
```bash
skillhub --version
```

当前最新版本：`skillhub 2026.3.13`

---

## 🚀 安装方法

### 方法 1：pip 安装（推荐）

```bash
pip install skillhub
```

### 方法 2：从源码安装

```bash
# 克隆仓库
git clone <skillhub-repo-url>
cd skillhub

# 安装
pip install -e .
```

### 方法 3：使用 pipx（隔离环境）

```bash
pipx install skillhub
```

---

## 🔧 基本使用

### 1. 搜索技能

```bash
skillhub search <关键词>
```

示例：
```bash
# 搜索 agent 相关技能
skillhub search agent

# 搜索 web 相关技能
skillhub search web

# 搜索 rust 相关技能
skillhub search rust
```

### 2. 安装技能

```bash
skillhub install <skill-slug>
```

示例：
```bash
# 安装多智能体编排技能
skillhub install agent-orchestrator-molter

# 安装 web 设计技能
skillhub install web-design

# 安装 agent 培训系统
skillhub install agent-training
```

**安装位置**：技能会安装到 `./skills/` 目录（默认），或使用 `--dir` 指定目录：
```bash
skillhub install <skill-slug> --dir /path/to/skills
```

### 3. 列出已安装技能

```bash
skillhub list
```

### 4. 升级技能

```bash
# 升级所有已安装的技能
skillhub upgrade

# 升级特定技能
skillhub upgrade <skill-slug>
```

### 5. 自升级 CLI

```bash
skillhub self-upgrade
```

---

## 📚 技能仓库策略

根据配置，有两个技能仓库：

| 仓库 | 用途 | 优先级 | 特点 |
|------|------|--------|------|
| **skillhub** | 国内优化源 | 🥇 优先 | 速度快，国内优化 |
| **clawhub** | 公共仓库 | 🥈 备用 | 全球访问，备选方案 |

**使用策略**：
1. ✅ 先尝试 `skillhub`（国内优化）
2. ⚠️ 如果不可用、限流或无匹配，回退到 `clawhub`

---

## 🎯 安装示例

### 示例 1：安装 agent-orchestrator-molter

```bash
skillhub install agent-orchestrator-molter
```

输出：
```
info: "agent-orchestrator-molter" not in index, using remote registry exact match
Downloading: https://lightmake.site/api/v1/download?slug=agent-orchestrator-molter
Installed: agent-orchestrator-molter -> /root/.openclaw/workspace/skills/agent-orchestrator-molter
```

### 示例 2：搜索 agent 相关技能

```bash
skillhub search agent
```

输出（部分）：
```
agent-orchestrator-molter  Agent Orchestrator
  - Multi-agent orchestration with 5 proven patterns - Work Crew, Supervisor, Pipeline, Council, and Auto-Routing
多智能体编排的5种成熟模式：工作组、主管、流水线、委员会与自动路由
  - version: 1.0.5

agent-training  Agent Training System
  - Agent培训系统 - 用于培训多Agent团队
  - version: 1.0.0

agent-dashboard  Agent Dashboard
  - Real-time agent dashboard for OpenClaw
  - version: 1.0.4
```

---

## 🛠️ 高级用法

### 指定安装目录

```bash
skillhub install <skill-slug> --dir /custom/path
```

### 指定索引文件

```bash
skillhub search <keyword> --index https://example.com/skills.json
```

### 跳过自升级检查

```bash
skillhub install <skill-slug> --skip-self-upgrade
```

---

## 📋 常用技能推荐

### AI Agent 相关

```bash
# 多智能体编排（5 种模式）
skillhub install agent-orchestrator-molter

# Agent 培训系统
skillhub install agent-training

# Agent 实时仪表板
skillhub install agent-dashboard

# Agent 浏览器自动化
skillhub install agent-browser
```

### Web 开发相关

```bash
# Web 设计系统
skillhub install web-design

# UI/UX 设计
skillhub search ui
```

### 编程语言相关

```bash
# Rust
skillhub search rust

# Python
skillhub search python

# TypeScript
skillhub search typescript
```

---

## ❓ 常见问题

### 1. 安装失败

**问题**：`pip install skillhub` 失败

**解决方案**：
```bash
# 升级 pip
pip install --upgrade pip

# 使用国内镜像
pip install skillhub -i https://pypi.tuna.tsinghua.edu.cn/simple
```

### 2. 找不到命令

**问题**：`skillhub: command not found`

**解决方案**：
```bash
# 检查 PATH
echo $PATH

# 添加到 PATH（临时）
export PATH=$PATH:/root/.local/bin

# 添加到 PATH（永久，添加到 ~/.bashrc）
echo 'export PATH=$PATH:/root/.local/bin' >> ~/.bashrc
source ~/.bashrc
```

### 3. 技能搜索无结果

**问题**：`skillhub search <keyword>` 无结果

**解决方案**：
```bash
# 尝试不同的关键词
skillhub search agent
skillhub search agents
skillhub search ai-agent

# 检查网络连接
ping lightmake.site
```

### 4. 安装目录权限问题

**问题**：`Permission denied`

**解决方案**：
```bash
# 使用 sudo（不推荐）
sudo skillhub install <skill-slug>

# 或指定用户目录
skillhub install <skill-slug> --dir ~/.skills
```

---

## 🔗 相关链接

- **ClawHub（公共仓库）**：https://clawhub.com
- **OpenClaw 社区**：https://discord.com/invite/clawd
- **OpenClaw 文档**：https://docs.openclaw.ai

---

## 📝 安装验证

安装后，运行以下命令验证：

```bash
# 检查版本
skillhub --version

# 搜索技能
skillhub search agent

# 安装一个测试技能
skillhub install agent-orchestrator-molter

# 列出已安装技能
skillhub list
```

---

## 🎯 快速开始

```bash
# 1. 安装 skillhub
pip install skillhub

# 2. 验证安装
skillhub --version

# 3. 搜索技能
skillhub search agent

# 4. 安装技能
skillhub install agent-orchestrator-molter

# 5. 列出已安装技能
skillhub list
```

---

## 📧 支持

如有问题，可以在 OpenClaw 社区寻求帮助：
- Discord：https://discord.com/invite/clawd
- GitHub：https://github.com/openclaw/openclaw

---

**文档版本**：1.0
**更新日期**：2026-03-18
**适用版本**：skillhub 2026.3.13+
