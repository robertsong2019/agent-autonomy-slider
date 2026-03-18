# 安全开发指南 - 防止敏感信息泄露

## 🚨 事故回顾（2026-03-18）

在创建 `agent-role-orchestrator` 项目时，整个 workspace 被提交到 GitHub，导致：
- Tavily API Key 泄露
- 腾讯文档 Token 泄露
- 个人信息泄露
- 所有已安装技能泄露

**根本原因**：在 workspace 目录下创建项目，使用 `git add -A` 提交了所有文件。

---

## ✅ 必须遵守的安全规则

### **规则 1：永远不要在 workspace 目录下创建项目**

```bash
# ❌ 错误
cd /root/.openclaw/workspace
mkdir my-project
cd my-project
git init

# ✅ 正确
cd /tmp  # 或 ~/projects
mkdir my-project
cd my-project
git init
```

**原因**：workspace 包含所有敏感文件，容易误提交。

---

### **规则 2：创建项目时必须先创建 .gitignore**

**步骤**：
```bash
# 1. 创建项目目录
cd /tmp
mkdir my-project
cd my-project

# 2. 初始化 Git
git init

# 3. 立即创建 .gitignore（在任何代码之前）
cat > .gitignore << 'EOF'
# 敏感文件 - 绝不要提交
TOOLS.md
MEMORY.md
USER.md
.env
.env.local
*.key
*.token
*_token
*_secret
credentials.json
secrets.json

# OpenClaw 敏感文件
.openclaw/
.clawhub/

# 操作系统文件
.DS_Store
Thumbs.db

# 编辑器
.vscode/
.idea/
*.swp

# 依赖
node_modules/
EOF

# 4. 提交 .gitignore
git add .gitignore
git commit -m "chore: Add .gitignore"
```

---

### **规则 3：提交前必须审查**

```bash
# ✅ 每次提交前都要检查
git status          # 查看要提交的文件
git diff            # 查看具体变更
git diff --cached   # 查看暂存的变更

# 确认无误后再提交
git commit -m "message"
```

**检查清单**：
- [ ] 没有包含 `TOOLS.md`, `MEMORY.md`, `USER.md`
- [ ] 没有包含 `.env` 文件
- [ ] 没有包含 `*.key`, `*.token` 文件
- [ ] 没有包含 `.openclaw/`, `.clawhub/` 目录
- [ ] 没有包含 API Key、Token、密码

---

### **规则 4：使用全局 .gitignore**

```bash
# 创建全局 .gitignore
cat > ~/.gitignore_global << 'EOF'
# 敏感文件
TOOLS.md
MEMORY.md
USER.md
.env
*.key
*.token
EOF

# 配置全局生效
git config --global core.excludesfile ~/.gitignore_global
```

---

### **规则 5：使用 pre-commit hook 自动检查**

```bash
# 在项目根目录创建 .git/hooks/pre-commit
cat > .git/hooks/pre-commit << 'EOF'
#!/bin/bash

# 检查是否有敏感文件
SENSITIVE_FILES="TOOLS.md MEMORY.md USER.md .env *.key *.token"

for file in $SENSITIVE_FILES; do
    if git diff --cached --name-only | grep -q "$file"; then
        echo "❌ 错误：检测到敏感文件 $file"
        echo "   请从提交中移除该文件"
        exit 1
    fi
done

# 检查是否有 API Key 模式
if git diff --cached | grep -qE "(tvly-|ghp_|sk-|token.*=.*[a-zA-Z0-9]{20,})"; then
    echo "❌ 错误：检测到可能的 API Key 或 Token"
    echo "   请检查提交内容"
    exit 1
fi

echo "✅ 安全检查通过"
EOF

chmod +x .git/hooks/pre-commit
```

---

## 🔧 标准项目创建流程

### **步骤 1：创建隔离的项目目录**

```bash
# 使用 /tmp 或 ~/projects
cd /tmp  # 或 cd ~/projects
mkdir my-project
cd my-project
```

### **步骤 2：初始化 Git 和 .gitignore**

```bash
git init
# 创建 .gitignore（参考上面的模板）
git add .gitignore
git commit -m "chore: Add .gitignore"
```

### **步骤 3：添加代码（不包含敏感信息）**

```bash
# 添加你的代码
echo "# My Project" > README.md
git add README.md
git status  # 检查
git commit -m "docs: Add README"
```

### **步骤 4：推送到 GitHub**

```bash
gh repo create my-project --public --source=. --remote=origin
git push -u origin main
```

---

## 🔍 敏感文件清单

**绝不要提交到 Git 的文件**：

| 文件 | 包含内容 | 风险级别 |
|------|---------|---------|
| `TOOLS.md` | API Keys, SSH hosts, TTS preferences | 🔴 高 |
| `MEMORY.md` | Tokens, personal info, project config | 🔴 高 |
| `USER.md` | Personal info, preferences | 🟡 中 |
| `.env` | Environment variables, secrets | 🔴 高 |
| `.openclaw/` | OpenClaw state, config | 🟡 中 |
| `.clawhub/` | Skill registry, locks | 🟡 中 |
| `*.key` | Private keys | 🔴 高 |
| `*.token` | Access tokens | 🔴 高 |
| `credentials.json` | Credentials | 🔴 高 |
| `secrets.json` | Secrets | 🔴 高 |

---

## 📋 检查清单

### **创建新项目时**
- [ ] 在隔离目录创建（/tmp 或 ~/projects）
- [ ] 立即创建 .gitignore
- [ ] 配置全局 .gitignore
- [ ] 设置 pre-commit hook
- [ ] 提交前审查 `git status`

### **每次提交前**
- [ ] 运行 `git status` 检查文件列表
- [ ] 运行 `git diff` 检查变更内容
- [ ] 确认没有敏感文件
- [ ] 确认没有 API Key/Token

### **推送到 GitHub 前**
- [ ] 再次确认没有敏感信息
- [ ] 考虑是否需要私有仓库
- [ ] 检查 Git 历史（`git log`）

---

## 🚨 应急响应流程

### **发现泄露时**
1. **立即删除文件**
   ```bash
   git rm <sensitive-file>
   git commit -m "security: Remove sensitive file"
   git push
   ```

2. **重新生成泄露的 Token**
   - Tavily API Key
   - GitHub Token
   - 其他相关 Token

3. **清理 Git 历史**（如果需要）
   ```bash
   # 使用 BFG Repo-Cleaner
   java -jar bfg.jar --delete-files <sensitive-file>
   git push --force
   ```

4. **通知相关方**
   - 用户
   - 服务提供商

---

## 📚 相关资源

- [GitHub - Remove sensitive data](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository)
- [Git - gitignore](https://git-scm.com/docs/gitignore)
- [BFG Repo-Cleaner](https://rtyley.github.io/bfg-repo-cleaner/)

---

**最后更新**：2026-03-18
**事故编号**：SEC-2026-0318-001
**严重级别**：🔴 严重（Critical）
