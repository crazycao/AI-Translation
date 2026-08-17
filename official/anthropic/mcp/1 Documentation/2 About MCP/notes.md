# 学习笔记 —— Architecture overview

## 核心概念自我复述

**host / client / server 三者关系**
容易把「MCP 客户端」和「AI 应用」混为一谈，实际上三者是包含关系：

- **MCP Host（宿主）** = 用户实际使用的 AI 应用本身（如 Claude Desktop、VS Code）。
- **MCP Client（客户端）**= 宿主内部创建的连接对象，每连接一个服务器就实例化一个客户端，一对一维护连接。
- **MCP Server（服务器）**= 真正提供上下文（数据/工具/提示词）的程序，可本地（stdio）或远程（Streamable HTTP）运行。

类比：宿主像一台电脑，客户端像它插出去的每一根数据线，服务器像线另一头连接的外设。一台电脑（宿主）可以同时插好几根线（客户端），分别接不同的外设（服务器）。

**数据层 vs 传输层**
- 数据层关心「说什么」：消息结构、语义、原语（tools/resources/prompts）、JSON-RPC 2.0 格式。
- 传输层关心「怎么传」：用 stdio 还是 HTTP、如何鉴权、如何分帧。
- 二者解耦的好处：换传输方式（本地 stdio 换成远程 HTTP）不需要改数据层协议，业务逻辑不受影响。

**Primitives（原语）是理解 MCP 的关键词**
- 服务器可暴露的三种原语：tools（能做什么）、resources（有什么数据）、prompts（怎么组织交互模板）。
- 客户端可暴露的原语：elicitation（向用户要更多信息）；sampling、logging 已在 2026-07-28 版本弃用，说明协议在往「不侵入宿主内部 LLM 调用逻辑」的方向演进——服务器不应该越权替宿主调用模型或抢占日志系统，而应直接对接 LLM 提供商 API / OpenTelemetry。

**无状态性（statelessness）的设计取舍**
每个请求都要自带协议版本、能力、身份信息（放在 `_meta` 里），不依赖连接上下文去推断。好处是服务器可以水平扩展、无需 session 亲和性；代价是每个请求都要重复携带一些元数据，好在协议设计了 `ttlMs`/`cacheScope` 允许发现结果被缓存，抵消这部分开销。

## 术语由来与易混点

- **Discovery vs Capabilities**：discovery 是「动作」（发一个 `server/discover` 请求去问），capabilities 是「结果」（问回来的能力清单）。文档里两者经常同时出现，翻译时要分清楚谁是动词谁是名词。
- **通知（Notifications）是 opt-in 的**：不是服务器有变化就无脑推给所有客户端，客户端必须先用 `subscriptions/listen` 声明自己要哪种通知，服务器才会推送——这与很多「默认全量推送、客户端自己过滤」的系统设计思路相反，更节省带宽。
- **resultType: "complete"**：目前只在 JSON 示例里看到这个字段，暗示可能存在「未完成/分页/流式」的其他 resultType（比如后面提到的 pagination、Tasks 扩展），值得后续读到相关章节时回来确认。

## 延伸阅读 / 待确认

- <!-- TODO: 想确认 `resultType` 除 "complete" 外还有哪些取值，等读到 pagination 或 Tasks 扩展章节时补充。 -->
- JSON-RPC 2.0 规范原文：https://www.jsonrpc.org/
- MCP 规范中「无状态性」章节：/specification/2026-07-28/basic/index#statelessness（相对路径，需在官方站点内跳转）
