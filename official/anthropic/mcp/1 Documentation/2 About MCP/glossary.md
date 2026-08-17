# 术语对照表 —— Architecture overview

本表收录《架构总览》（Architecture overview）一文中出现的核心术语，仅覆盖本文范围。全站汇总请见 [../glossary速查.md](../glossary速查.md)。

| English | 中文译法 | 说明 |
|---|---|---|
| MCP Host | MCP 宿主 | 协调、管理一个或多个 MCP 客户端的 AI 应用，如 Claude Code、Claude Desktop、VS Code |
| MCP Client | MCP 客户端 | 宿主为每个 MCP 服务器创建的组件，维持一条专用连接 |
| MCP Server | MCP 服务器 | 向客户端提供上下文的程序，可本地或远程运行 |
| Data layer | 数据层 | 定义基于 JSON-RPC 的通信协议、核心原语 |
| Transport layer | 传输层 | 定义连接建立、消息分帧、鉴权等通信机制 |
| Stdio transport | Stdio 传输 | 基于标准输入/输出流的本地进程通信方式 |
| Streamable HTTP transport | Streamable HTTP 传输 | 基于 HTTP POST + 可选 SSE 的远程通信方式 |
| Primitives | 原语 | MCP 中最核心的概念，定义客户端与服务器可以彼此提供的内容 |
| Tools | 工具 | 服务器原语之一，AI 可调用以执行动作的可执行函数 |
| Resources | 资源 | 服务器原语之一，提供上下文信息的数据源 |
| Prompts | 提示词 | 服务器原语之一，用于结构化交互的可复用模板 |
| Elicitation | 征询 | 客户端原语，允许服务器向用户请求额外输入或确认 |
| Sampling | 采样 | 客户端原语（已弃用），允许服务器请求 LLM 补全 |
| Logging | 日志记录 | 客户端原语（已弃用），服务器向客户端发送日志消息 |
| Notifications | 通知 | 服务器向客户端推送的实时更新消息，无需响应 |
| Discovery | 发现 | 客户端查询服务器支持的版本、能力与身份的过程 |
| Capabilities | 能力 | 客户端或服务器所支持的特性与操作 |
| Statelessness | 无状态性 | 每个请求自带处理所需的全部信息，服务器不依赖此前请求 |
| Extensions | 扩展 | 在核心协议之上构建的可选功能，如 Tasks 扩展 |
| Durable handle | 持久句柄 | Tasks 扩展中，服务器为长时间运行请求返回的可轮询凭据 |
| Subscription | 订阅 | 客户端通过 `subscriptions/listen` 建立的长连接通知流 |
