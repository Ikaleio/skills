# Codex Skills

本仓库保存 Ikaleio 使用的用户级全局 skills。当前内容同步自本机的非系统 skill 目录，快照日期为 2026-08-28。

仓库不包含 Codex 内置的 `.system` skills，也不包含插件缓存。

## Skills

| 名称 | 用途 |
| --- | --- |
| `agent-browser` | 通过命令行自动操作浏览器和 Electron 应用。 |
| `grill-me` | 逐项追问并检验计划或设计中的决策。 |
| `image-to-code` | 先生成和分析设计图，再实现视觉要求较高的网站。 |
| `ikadesign` | 设计和实现信息密度合理、响应式且可验收的生产级界面。 |
| `notion-spec-to-implementation` | 把 Notion 规格转换为实施计划、任务和进度记录。 |
| `shadcn` | 管理、检索、调试和组合 shadcn/ui 组件。 |
| `ste-writing` | 用受控技术写作规则编写或审查技术文本。 |
| `v0-design-guidelines` | 在通用 Agent 环境中应用 v0 风格的界面设计规则。 |

## 安装

[skills CLI](https://www.skills.sh/docs/cli) 可以直接从 GitHub 安装本仓库中的 skills。使用 Bun 将需要的 skills 安装到 Codex 的用户级全局目录：

```bash
bunx skills add Ikaleio/skills --global --agent codex
```

安装全部 skills，并跳过交互确认：

```bash
bunx skills add Ikaleio/skills --global --agent codex --skill '*' --yes
```

更新已安装的全局 skills：

```bash
bunx skills update --global
```

## 许可

部分 skill 包含或改编自第三方材料。各文件保留其原有版权说明和许可文件。本仓库不对全部内容授予统一许可。
