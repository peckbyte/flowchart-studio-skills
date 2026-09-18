# flowchart-studio-skills

流程图工坊（[flowchart.e3e4.club](https://flowchart.e3e4.club)）的 Agent 插件包：`mcp.json` 连接器 + `skills/`，结构对齐 [GitbookIO/gitbook-skills](https://github.com/GitbookIO/gitbook-skills)。

装好后应显示 **1 个连接器 · 2 个技能**（operate-studio / http-api）。

## 仓库里有什么

| 路径 | 作用 |
| --- | --- |
| `mcp.json` / `.mcp.json` | Streamable HTTP → `https://flowchart.e3e4.club/mcp` |
| `plugin.json` | Agent Plugins 根清单 |
| `.cursor-plugin/` | Cursor 插件（含 `FLOWCHART_API_TOKEN` 变量） |
| `.grok-plugin/` | Grok 插件清单 |
| `.claude-plugin/` | Claude 风格 marketplace + MCP |
| `skills/operate-studio` | 优先走 MCP 工具 |
| `skills/http-api` | HTTP `/api/v1` 后备 |

## Grok Bot 安装（推荐）

1. 在 Grok Bot **你的插件**里，删掉旧的 `flowchart-studio`（没有「连接器」的那条）。
2. 用 GitHub 仓库重装：
   - 发现 / 插件 → 从 GitHub 添加，填 `peckbyte/flowchart-studio-skills`  
   - 或在对话里说：`安装 GitHub 插件 peckbyte/flowchart-studio-skills`
3. 安装后应出现 **1 个连接器**；点 **Authenticate / Configure**，填入网站设置里的 `fst_…`。
4. 新开对话，问「有哪些 Cursor 桥 / 连接器」，应能看到 flowchart-studio。

## Cursor 本地调试

```bash
mkdir -p ~/.cursor/plugins/local
git clone https://github.com/peckbyte/flowchart-studio-skills.git ~/.cursor/plugins/local/flowchart-studio
```

然后 `Developer: Reload Window`，在 Customize → Plugins 查看；Configure 填写 `FLOWCHART_API_TOKEN`。

也可：

```bash
npx skills add peckbyte/flowchart-studio-skills -y
```

## 鉴权

仓库**不含**钥匙。`mcp.json` 使用：

```json
"Authorization": "Bearer ${FLOWCHART_API_TOKEN}"
```

## License

MIT
