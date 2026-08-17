# MCP 术语速查表

本表汇总 `official/anthropic/mcp/` 站点下所有已翻译页面中出现的术语，按拼音/字母顺序排列，用于跨文档快速查找、保持全站译法统一。

各页面正文旁的 `glossary.md` 只收录该单篇文档涉及的术语；本文件是全站汇总，新增术语时请同步补充到这里。

## 使用说明

- 新翻译一篇文档、遇到未收录的术语时，请在此表补充一行，并在「出处」列标注来源页面。
- 同一术语若在不同文档中出现译法分歧，以本表为准；发现分歧应回头统一，并在「备注」列说明。

## 术语表

| English | 中文译法 | 备注 | 出处 |
|---|---|---|---|
| Agent | 智能体 | | 1 What is MCP |
| Capabilities | 能力 | 客户端/服务器所支持的特性与操作 | 1 Architecture |
| Client | 客户端 | 见 MCP Client | 1 What is MCP / 1 Architecture |
| Data layer | 数据层 | MCP 两层架构之一，内层 | 1 Architecture |
| Discovery | 发现 | 客户端查询服务器版本/能力/身份的过程；注意与「Capabilities」区分（动作 vs 结果） | 1 Architecture |
| Durable handle | 持久句柄 | Tasks 扩展中，服务器为长时间运行请求返回的可轮询凭据 | 1 Architecture |
| Ecosystem | 生态（系统） | | 1 What is MCP |
| Elicitation | 征询 | 客户端原语，服务器借此向用户请求额外输入或确认 | 1 Architecture |
| End-user | 最终用户 | | 1 What is MCP |
| Extensions | 扩展 | 构建于核心协议之上的可选功能，如 Tasks 扩展 | 1 Architecture |
| Host / MCP Host | 宿主 / MCP 宿主 | 用户实际使用的 AI 应用本身，如 Claude Code、Claude Desktop | 1 Architecture |
| Logging | 日志记录 | 客户端原语（协议版本 2026-07-28 起已弃用） | 1 Architecture |
| MCP（Model Context Protocol） | 模型上下文协议 | 首次出现标注英文全称，正文中简称 MCP | 1 What is MCP |
| MCP Client | MCP 客户端 | 宿主为每个服务器创建的连接组件，一对一维护连接 | 1 Architecture |
| MCP Server | MCP 服务器 | 提供上下文的程序，可本地（stdio）或远程（HTTP）运行 | 1 Architecture |
| Notifications | 通知 | 服务器向客户端推送的实时更新，无需响应；采用按需订阅（opt-in）机制 | 1 Architecture |
| Open-source standard | 开源标准 | | 1 What is MCP |
| Prompts | 提示词 | 服务器原语之一：可复用的交互结构模板 | 1 Architecture |
| Primitives | 原语 | MCP 中最核心的概念，定义 client/server 间可提供的内容类型 | 1 Architecture |
| Resources | 资源 | 服务器原语之一：提供上下文信息的数据源 | 1 Architecture |
| Sampling | 采样 | 客户端原语（协议版本 2026-07-28 起已弃用） | 1 Architecture |
| Server | 服务器 | 见 MCP Server | 1 What is MCP / 1 Architecture |
| Statelessness | 无状态性 | 每个请求自带处理所需的全部信息，服务器不依赖此前请求 | 1 Architecture |
| Streamable HTTP transport | Streamable HTTP 传输 | 基于 HTTP POST + 可选 SSE，支持远程通信 | 1 Architecture |
| Stdio transport | Stdio 传输 | 基于标准输入/输出流的本地进程通信方式 | 1 Architecture |
| Subscription | 订阅 | 客户端通过 `subscriptions/listen` 建立的长连接通知流 | 1 Architecture |
| Tools | 工具 | 服务器原语之一：AI 可调用以执行动作的可执行函数 | 1 Architecture / 1 What is MCP |
| Transport layer | 传输层 | MCP 两层架构之一，外层：连接建立、消息分帧、鉴权 | 1 Architecture |
| Workflow | 工作流 | | 1 What is MCP |

## 待观察 / 尚未统一的译法

<!-- 若某术语在多篇文档中出现不同译法，先记录在这里，讨论后再统一收进上表。 -->

（暂无）
