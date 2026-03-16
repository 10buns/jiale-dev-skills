<div align="center">

# Claude Code 配置

> 个人使用的 Claude Code 规则 / 技能集合  
> 只包含 `.claude/` 目录，方便直接同步到 `~/.claude/`

</div>

---

## 仓库定位

- 作者：**jiale.wang**
- 用途：为个人项目提供统一的 Claude Code 配置（规则、技能、commands）
- 范围：**仅包含 `.claude/` 相关内容**，不包含其它脚本或工具配置

目录结构：

```bash
jiale-dev-skills/
├── .claude/          # Claude Code 核心配置（从 cc-use-exp 精简而来）
└── README.md
```

---

## 使用方式

在仓库根目录执行（macOS / Linux）：

```bash
cp -R .claude ~/.claude
```

> 如需按需合并已有配置，可以只拷贝其中的 `rules/`、`skills/` 或 `commands/` 子目录。

---

## 注意事项

- 本仓库只针对 **Claude Code**

