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

## 项目配置

### Hourly Web Games
- **仓库**: https://github.com/robertsong2019/hourly-web-games
- **功能**: 每小时自动生成一个网页小游戏
- **Cron**: OpenClaw 内部 cron（`openclaw cron list` 查看）
- **Cron ID**: `2b8f4a14-6c3e-4572-a9f6-c3efaf402244`
- **脚本**: `/root/projects/hourly-web-games/generate-game.sh`
- **日志**: OpenClaw 统一日志
- **通知**: 通过飞书通知结果
- **当前游戏数**: 2（贪吃蛇、记忆翻牌）
- **下次运行**: 每小时整点

**注意**: 使用 OpenClaw 内部 cron，不是系统级 `/etc/cron.d/`

---

## 开发规范

### 新建工程必须包含
每次创建新项目时，必须包含以下文件：
- ✅ `README.md` - 项目说明文档
- ✅ `.gitignore` - Git 忽略规则

### 常用 .gitignore 模板

**Python 项目**:
```
__pycache__/
*.py[cod]
*$py.class
*.so
.Python
build/
develop-eggs/
dist/
downloads/
eggs/
.eggs/
lib/
lib64/
parts/
sdist/
var/
wheels/
*.egg-info/
.installed.cfg
*.egg
.env
.venv
env/
venv/
ENV/
```

**Node.js 项目**:
```
node_modules/
npm-debug.log*
yarn-debug.log*
yarn-error.log*
.env
dist/
build/
```

---

## 技能配置

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
- **Cron 配置**: `openclaw cron list` 查看
- **脚本**: `/root/projects/hourly-web-games/generate-game.sh`
- **日志**: OpenClaw 统一日志
- **通知**: 飞书 → Robert
- **当前游戏数**: 3 (贪吃蛇、记忆翻牌、2048)

### LKA（车道保持辅助）需求文档
- **仓库**: https://github.com/robertsong2019/lka-requirements
- **文档**: `/root/projects/LKA-Requirements.md`
- **创建时间**: 2026-03-16
- **功能**: LKA + ELK 车道保持辅助系统
- **方法**: 使用 brainstorming skill 梳理需求
- **状态**: ✅ 已完成并推送到 GitHub
- **关键决策**:
  - 功能范围: LKA + ELK
  - 激活方式: 混合模式（默认关闭，记住状态）
  - 感知方案: 摄像头 + 毫米波雷达
  - 控制策略: 力矩控制
  - 速度范围: 60-120 km/h
  - 退出机制: 分级退出（警告 → 降级 → 退出）
  - 人机交互: 视觉 + 声音
  - 接管逻辑: 暂停控制
