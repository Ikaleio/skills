# Codex Skills

本仓库保存 Ikaleio 使用的用户级全局 skills。当前内容同步自本机的非系统 skill 目录，快照日期为 2026-08-10。

仓库不包含 Codex 内置的 `.system` skills，也不包含插件缓存。

## Skills

| 名称 | 用途 |
| --- | --- |
| `agent-browser` | 通过命令行自动操作浏览器和 Electron 应用。 |
| `grill-me` | 逐项追问并检验计划或设计中的决策。 |
| `image-to-code` | 先生成和分析设计图，再实现视觉要求较高的网站。 |
| `notion-spec-to-implementation` | 把 Notion 规格转换为实施计划、任务和进度记录。 |
| `shadcn` | 管理、检索、调试和组合 shadcn/ui 组件。 |
| `ste-writing` | 用受控技术写作规则编写或审查技术文本。 |
| `v0-design-guidelines` | 在通用 Agent 环境中应用 v0 风格的界面设计规则。 |

## 安装

[Codex 官方文档](https://developers.openai.com/codex/skills)指定 `$HOME/.agents/skills` 为用户级 skill 目录，并支持符号链接。

先克隆仓库：

```bash
git clone https://github.com/Ikaleio/skills.git "$HOME/.local/share/ikaleio-codex-skills"
mkdir -p "$HOME/.agents/skills"
```

再安装需要的 skill：

```bash
ln -s \
  "$HOME/.local/share/ikaleio-codex-skills/ste-writing" \
  "$HOME/.agents/skills/ste-writing"
```

如需安装其他 skill，请替换命令中的目录名。如果目标目录已经存在，请先检查并备份现有内容。

更新仓库后，符号链接会直接使用新内容：

```bash
git -C "$HOME/.local/share/ikaleio-codex-skills" pull --ff-only
```

## 许可

部分 skill 包含或改编自第三方材料。各文件保留其原有版权说明和许可文件。本仓库不对全部内容授予统一许可。
