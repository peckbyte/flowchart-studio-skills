# flowchart-studio-skills

流程图工坊（[flowchart.e3e4.club](https://flowchart.e3e4.club)）的 **Agent 插件包**：MCP 连接器 + 操作技能。结构对齐 [GitbookIO/gitbook-skills](https://github.com/GitbookIO/gitbook-skills)，供 Cursor / Grok 等安装后出现「连接器 + 技能」，而不是只靠手工 `AddMcpServer`。

## 包含什么

| 组件 | 说明 |
| --- | --- |
| `mcp.json` | Streamable HTTP → `https://flowchart.e3e4.club/mcp` |
| `skills/operate-studio` | 优先走 MCP 工具改图 |
| `skills/http-api` | 无 MCP 时的 `/api/v1` 后备说明 |
| `.cursor-plugin/` | Cursor 插件清单（含 `FLOWCHART_API_TOKEN` 变量） |
| `.grok-plugin/` | Grok 插件清单 |

## 鉴权

插件**不**内置钥匙。在 Cursor：**Plugins → 流程图工坊 → Configure**，填入网站「设置」生成的 `fst_…`。  
`mcp.json` 使用：

```json
"Authorization": "Bearer ${FLOWCHART_API_TOKEN}"
```

## 本地安装（私有仓）

```bash
mkdir -p ~/.cursor/plugins/local
git clone git@github.com:peckbyte/flowchart-studio-skills.git ~/.cursor/plugins/local/flowchart-studio
```

然后在 Cursor 重载窗口，打开插件配置填入 token，确认 MCP `flowchart-studio` 为 connected。

也可继续用账户级连接器 `user-flowchart-studio`；本插件的目标是让 **Grok 技能页出现带连接器的 Cursor 桥**（对标 gitbook-cursor）。

## 许可证

MIT
