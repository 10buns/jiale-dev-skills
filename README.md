<div align="center">

# Claude Code 配置（精简版）

</div>

> 基于 [cc-use-exp](https://github.com/doccker/cc-use-exp) 提取的 **Claude Code** 配置，仅保留 `.claude/` 相关内容  
> 按费力度从低到高，用最少操作获得最大帮助

---

## 项目简介


```text
本仓库                     用户目录
├── .claude/  ──覆盖──>   ~/.claude/
```

- **本仓库**：只维护 Claude Code 的配置，不参与实际业务开发
- **用户目录**：实际生效的配置（`~/.claude/`）

---

## Claude Code 配置概览

### 目录结构

```bash
~/.claude/
├── CLAUDE.md          # 核心配置（本地使用时覆盖到这里）
├── rules/             # 规则（部分按 paths 按需加载）
│   ├── claude-code-defensive.md
│   ├── ops-safety.md
│   ├── doc-sync.md
│   ├── bash-style.md
│   └── date-calc.md
├── skills/            # 按需加载的技能
│   ├── java-dev/
│   ├── frontend-dev/
│   ├── python-dev/
│   ├── bash-style/
│   ├── ops-safety/
│   └── size-check/
└── commands/          # 用户命令
    ├── fix.md
    ├── review.md
    ├── design.md
    ├── project-init.md
    ├── project-scan.md
    ├── style-extract.md
    ├── requirement.md
    ├── commit-msg.md
    ├── status.md
    └── check-toolsearch.md
```

---

## 1. 快速开始

### 1.1 零费力（自动生效）- Rules

**你需要做什么：什么都不用做**

这些规则始终自动加载，在后台默默保护你：

| 规则 | 作用 | 触发场景 |
|------|------|---------|
| `claude-code-defensive.md` | 防止测试篡改、过度工程化、中途放弃 | 始终生效 |
| `ops-safety.md` | 危险命令确认、回滚方案、风险提示 | 始终生效（详细规范见 skills） |
| `doc-sync.md` | 配置/结构变更时提醒更新文档 | 修改配置时 |
| `bash-style.md` | Bash 核心规范：禁止行尾注释 | 始终生效（详细规范见 skills） |
| `date-calc.md` | 日期加减保持日不变，禁止默认月末对齐 | 始终生效 |

**效果示例：**
- Claude 不会修改测试来适配错误代码
- 执行 `sysctl` 等危险命令前会提示风险和回滚方案
- 新增命令后会提醒你更新 README

### 1.2 低费力（自动触发）- Skills

**你需要做什么：正常写代码**

操作相关文件时自动加载对应的开发规范：

| 技能 | 触发条件 | 提供的帮助 |
|------|---------|-----------|
| `java-dev` | 操作 `.java` 文件 | 命名约定、异常处理、Spring 规范等 |
| `frontend-dev` | 操作 `.vue/.tsx/.css` 等 | UI 风格约束、Vue/React 规范、TypeScript |
| `python-dev` | 操作 `.py` 文件 | 类型注解、pytest 等 |
| `bash-style` | 操作 `.sh/Dockerfile/Makefile/.md` 等 | 注释规范、heredoc、脚本规范 |
| `ops-safety` | 执行系统命令、服务器运维 | 风险说明、回滚方案、问题排查原则 |
| `size-check` | `/size-check` 或描述“简化代码” | 代码简化审查、全项目文件行数扫描 |

### 1.3 中费力（显式调用）- Commands

**你需要做什么：输入 `/命令名`**

#### 高频命令（日常使用）

| 命令 | 用途 | 使用示例 |
|------|------|---------|
| `/fix` | 快速修复 Bug | `/fix 登录接口返回 500` |
| `/fix debug` | 复杂问题排查（复现→假设→验证→修复） | `/fix debug 定时任务不执行` |
| `/review` | 正式代码审查 | `/review` |
| `/review quick` | 快速审查（git diff + 简要意见） | `/review quick` |
| `/commit-msg` | 生成 git commit message | `/commit-msg` 或 `/commit-msg all` |

#### 中频命令（按需使用）

| 命令 | 用途 | 使用示例 |
|------|------|---------|
| `/review security` | 安全审查当前分支代码 | `/review security` |
| `/new-feature` | 新功能全流程（需求→设计→实现） | `/new-feature 用户导出功能` |
| `/design doc` | 生成技术设计文档框架 | `/design doc 用户权限模块` |
| `/requirement doc` | 生成需求文档框架 | `/requirement doc 报表功能` |

#### 低频命令（特定场景）

| 命令 | 用途 | 使用示例 |
|------|------|---------|
| `/requirement interrogate` | 需求极刑审问，挖掘逻辑漏洞 | `/requirement interrogate 用户要导出数据` |
| `/design checklist` | 生成设计质量检查清单 | `/design checklist` |
| `/project-init` | 为新项目初始化 Claude Code 配置 | `/project-init` |
| `/project-scan` | 扫描项目生成配置（CLAUDE.md/restart.sh/ignore/Docker） | `/project-scan` |
| `/style-extract` | 从代码或设计图提取样式变量 | `/style-extract` |
| `/check-toolsearch` | 检查 ToolSearch/WebSearch 是否可用 | `/check-toolsearch` |
| `/status` | 显示当前配置状态（Rules/Skills/LSP） | `/status` |

---

## 2. 常见场景速查（Claude Code）

| 场景 | 推荐方式 | 费力度 |
|------|---------|--------|
| 日常写代码 | 直接写，Rules + Skills 自动生效 | ⭐ |
| 修个小 Bug | `/fix 问题描述` | ⭐⭐ |
| 提交前快速看看 | `/review quick` | ⭐⭐ |
| 生成 commit message | `/commit-msg` | ⭐⭐ |
| 正式代码审查 | `/review` | ⭐⭐ |
| 复杂 Bug 排查 | `/fix debug 问题描述` | ⭐⭐⭐ |
| 安全审查 | `/review security` | ⭐⭐⭐ |
| 开发新功能 | `/new-feature 功能名` | ⭐⭐⭐ |
| 新项目初始化 | `/project-init` | ⭐⭐⭐ |

---

## 3. 使用方式（本仓库）

在本仓库根目录执行（macOS / Linux）：

```bash
cp -R .claude ~/.claude
```

> 如需按需合并已有配置，可以只拷贝其中的 `rules/`、`skills/` 或 `commands/` 子目录。

---

## 注意事项

