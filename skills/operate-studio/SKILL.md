---
name: operate-studio
metadata:
  version: "1.0"
description: >-
  use this when 用户要通过 MCP/连接器操作流程图工坊（flowchart-studio）：列分组与图、建改删图、评论、
  节点关联、主题、回滚。优先调用 flowchart-studio MCP 工具，不要只改本地文件。
---

# 操作流程图工坊（MCP）

## 何时用

用户说「画/改流程图」「列工坊里的图」「给节点挂 Notion/飞书」「按评论改图」等，且本会话已安装 **flowchart-studio** 插件（带 MCP 连接器）时使用本技能。

## 连接器

- MCP：`flowchart-studio`（`https://flowchart.e3e4.club/mcp`）
- 鉴权：插件变量 `FLOWCHART_API_TOKEN` → `Authorization: Bearer fst_…`
- 无钥时：请用户在网站「设置」生成钥匙，在 Cursor **Plugins → 流程图工坊 → Configure** 填入；不要让用户把完整钥匙贴进聊天。

## 推荐调用顺序

1. 陌生环境先 `agent_capabilities` / `list_kinds` / `list_groups`。
2. 改图前先 `get_flowchart_context`（或 `list_flowcharts`），记下 `version`。
3. 小改优先 `apply_mutations`；整页替换用 `update_flowchart`（mermaid | diagram | html 三选一）。
4. 所有写操作必须带当前 `version`；若 `409 VERSION_CONFLICT`，重新 GET 再写。
5. 删图/删分组必须 `confirm=true`，并先口头确认用户意图。
6. 评论：`create_comment` 才会触发分组 webhook；`apply_comment` 用于落地 change_request。

## 常用工具

| 目的 | 工具 |
| --- | --- |
| 能力/类型 | `agent_capabilities`, `list_kinds` |
| 分组 | `list_groups`, `delete_group` |
| 列/读图 | `list_flowcharts`, `get_flowchart_context` |
| 建图 | `create_flowchart`（mermaid \| diagram \| html 之一） |
| 改图 | `apply_mutations`, `update_flowchart` |
| 删图 | `delete_flowchart` |
| 预览转换 | `convert` |
| 评论 | `list_comments`, `create_comment`, `apply_comment` |
| 节点 | `list_nodes`, `get_node`, `put_node` |
| 主题 | `list_themes` |
| 历史 | `list_revisions`, `restore_revision` |

## 图类型

`flowchart` | `architecture` | `state_machine` | `swimlane` | `hierarchy` | `matrix`

节点关联 `links[].type`：`notion` | `feishu` | `local` | 自定义小写。

## 不做

- 不把 API 钥匙、webhook secret 写进仓库或聊天。
- 不上机改 Docker/证书（那是运维职责）；本技能只经 MCP/API 改图数据。
- 不把 HTML 以外的渲染引擎当成原稿；HTML 是画面权威来源。
