# Skills

Ikaleio 自用的 Agent skills。每个顶层目录是一个 skill，入口文件是该目录下的 `SKILL.md`。

## Skills

| 名称 | 用途 |
| --- | --- |
| [`finetone`](finetone/SKILL.md) | 发消息前按固定流程找出用户最容易漏掉的要害，再用先说结论、讲清因果、口语化的方式写进度和最终回复。 |
| [`grill-me`](grill-me/SKILL.md) | 逐项追问计划或设计，直到每个决策分支都有结论。 |
| [`ikadesign3`](ikadesign3/SKILL.md) | 从现有前端代码、网站或截图提取 design.md，按品牌要求创建 design.md，或按 design.md 实现和审查页面。design.md 只描述 UI 呈现，不描述产品功能。 |
| [`ste-writing`](ste-writing/SKILL.md) | 按 ASD-STE100 派生的受控规则编写、改写或审查技术文本。 |

## 安装

### Codex 和 Claude Code

用 [skills CLI](https://www.skills.sh/docs/cli) 从 GitHub 安装到用户级全局目录。不带 `--skill` 时，CLI 会让你选择要安装的 skills：

```bash
bunx skills add Ikaleio/skills --global --agent codex claude-code
```

安装全部 skills，并跳过确认：

```bash
bunx skills add Ikaleio/skills --global --agent codex claude-code --skill '*' --yes
```

更新已安装的全局 skills：

```bash
bunx skills update --global
```

### omp

skills CLI 不支持 omp。把仓库克隆到 omp 的用户级 skills 目录：

```bash
git clone https://github.com/Ikaleio/skills ~/.omp/agent/skills
```

更新：

```bash
git -C ~/.omp/agent/skills pull
```

## 添加 skill

1. 新建 `<name>/SKILL.md`。
2. 在 frontmatter 中写 `name` 和 `description`。`name` 与目录名一致。
3. 运行 `bunx skills add . --list`，确认 CLI 能识别新 skill。

## 许可

部分 skill 包含或改编自第三方材料。本仓库不对全部内容授予统一许可。
