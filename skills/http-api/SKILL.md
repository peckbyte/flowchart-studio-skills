---
name: http-api
metadata:
  version: "1.0"
description: >-
  use this when 没有 MCP 连接器、只能用 HTTP 调 flowchart-studio /api/v1：建改删图与分组、评论、
  节点关联、主题、回滚。有 MCP 时优先用 operate-studio。
---

# 流程图工坊 HTTP API

线上前缀：`https://flowchart.e3e4.club/api/v1`  
鉴权：`Authorization: Bearer fst_…`（环境变量如 `FLOWCHART_API_TOKEN` / `FLOWCHART_STUDIO_TOKEN`）

## 写操作纪律

- 改图内容必须带当前 `version` 或头 `If-Match`；冲突 `409` 先 GET 再重试。
- 可带 `Idempotency-Key`。
- HTML 是原稿；mermaid / diagram 只是输入，一次只送一种。

## 速查

| 目的 | 方法 |
| --- | --- |
| 能力 | `GET /agent/capabilities` |
| 类型 | `GET /kinds` |
| 转换不存盘 | `POST /convert` |
| 建图 | `POST /flowcharts` |
| 列表 | `GET /flowcharts` |
| 上下文 | `GET /flowcharts/:id/context` |
| 局部改 | `POST /flowcharts/:id/mutations` |
| 整页/主题 | `PATCH /flowcharts/:id` |
| 删图 | `DELETE /flowcharts/:id` |
| 评论 | `GET\|POST /flowcharts/:id/comments` |
| 节点 | `GET\|PUT\|PATCH /flowcharts/:id/nodes/:nodeId` |
| 分组 | `GET\|POST /groups`，`PATCH\|DELETE /groups/:id` |
| 回滚 | `GET .../revisions`，`POST .../revisions/:n/restore` |
| 主题 | `GET\|POST /themes` |

人看文档：`/api/docs`（需登录）。OpenAPI：`GET /api/v1/openapi.json`（需 Bearer）。
