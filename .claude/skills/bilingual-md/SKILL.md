---
name: bilingual-md
description: Use when the user asks to add Chinese translations to an English Markdown document in this repo (e.g. "在这个文件中每一段英文之后加它的中文翻译"), or to produce a Chinese-only companion file (e.g. "生成一个 (CN) 文件"、"根据我检查过的内容制作一个 (CN) 文件"). 
---

# 双语 Markdown 翻译约定（本项目专用）

> **仅供本项目 (`/Users/cwf/Code/translation`) 使用。**
> 该 skill 记录的是本仓库特有的双文件翻译约定与术语表。如果需要在其他项目复用这套流程，请另起一个 skill 名称（例如 `bilingual-md-{project}`），并按需修改术语表和目录规则，避免把本项目的选择带到其他仓库。

## Overview / 用途

本工程收录的英文原文文档，统一按以下双文件约定翻译：

1. **`{Name}.md`（双语对照版）**：保留全部原文，在每个英文块之后紧跟中文翻译。用户会逐段审阅并修改。
2. **`{Name} (CN).md`（纯中文版）**：等到用户审阅完双语版之后，再基于双语版中的中文内容生成，只保留中文，不带任何英文原文。

**关键原则**：CN 文件必须**基于用户已经审阅（可能已手动修订）过的双语版**来生成，而不是重新翻译。生成前先 `Read` 一次最新的双语文件。

## When to Use / 触发条件

- 用户明确要求"每段英文之后加中文翻译"、"翻译这个文件"、"加中文对照"等。
- 用户明确要求"生成一个 CN 文件"、"做个纯中文版本"、"根据我检查过的内容做 (CN)"。
- IDE 打开的是 `Others/` 或其他英文文档目录下的 `.md` / `.mdx` 文件。

不适用：仅要求翻译一个词/一句话；或要求把中文翻译成英文。

## Two-file workflow / 两步工作流

```
step1: 生成双语版           step2: 用户逐段审阅并可能手动修订
{Name}.md (EN + 中文)  →   ...  →  {Name} (CN).md (纯中文)
```

- 第 1 步产物：双语文件。用户会在 IDE 中修订（如把 `## Foo` 改成 `## Foo - 中文`、把 `` `name` `` 后加"（名称）"等）。
- 第 2 步产物：CN 文件。生成时**先 Read 一次最新的双语文件**，然后按下面的"CN 文件生成规则"提取中文。

## Bilingual formatting rules / 双语版格式规则

### 顶部

- 在一级标题之后（正文之前）加一行原文地址：
  ```
  原文地址：[https://…](https://…)
  ```
  如果不知道 URL，可省略这一行或询问用户。

### 标题

- **一级标题**：`# English Title 中文标题`（同行、空格分隔），或 `# English - 中文`。
- **二级及以下**：`## English Title - 中文标题`（同行、` - ` 分隔）。
- **字段/目录类小标题**：在中文侧对反引号里的关键词补一个中文含义括注：
  - `` #### `name` field - `name`（名称）字段 ``
  - `` ### `scripts/` （脚本） ``
  - `` ### `references/` （参考资料） ``
- 顶层标题的中文含义括注示例：`（描述）`、`（许可证）`、`（兼容性）`、`（参考资料）`、`（静态资源）`。

#### 标题序号

**默认**给正文各级标题加层级序号（`#` 全文标题除外）：

- `#`（H1，全文标题）**不加**序号。
- `##`（H2）：`1.`、`2.`、`3.` …… 数字后跟一个句点和一个空格，再接原标题内容。
- `###`（H3）：`1.1`、`1.2`、`2.1` …… 中间用 `.` 分隔，末尾**不加**句点，再接一个空格。
- `####`（H4）：`1.1.1` 依此类推。
- 序号加在英文标题之前：`## 3. Designing trigger eval queries - 设计用于触发评估的查询集`。
- 双语版和 CN 版都要加，且编号保持一致。

例：
```
# Optimizing skill descriptions - 优化 skill 描述        ← 不加序号
## 1. How skill triggering works - skill 触发机制
## 2. Writing effective descriptions - 编写有效的 description
## 3. Designing trigger eval queries - 设计用于触发评估的查询集
### 3.1 Should-trigger queries - 应触发的查询
### 3.2 Should-not-trigger queries - 不应触发的查询
## 4. Testing whether a description triggers - 测试 description 是否会触发
### 4.1 Running multiple times - 多次运行
```

若用户明确要求"不要加序号"，才跳过此步骤。

### 段落 / 列表 / 引用块

- **段落**：一段英文 → 空行 → 一段中文。**不要**逐行插入。
- **列表**：整块英文列表 → 空行 → 整块中文列表（顺序、层级一一对应）。**不要**拆到每一 bullet 后面。
- **引用块 `>`**：整段英文引用 → 空行 → 整段中文引用。

### 表格

- 先放完整英文表格，空行后放完整中文表格；表头也翻译。

### 代码块

- **原样保留原英文代码块**。
- 如果代码块里含有可翻译内容（英文注释、`description:` 里的英文文案、markdown 正文的英文说明），**再追加一份中文版本**：只翻译注释/文案，命令、YAML 键、参数名、shell 语法保持不变。
- 如果代码块只有纯键值（如 `metadata: {author, version}`）或纯命令（如 `skills-ref validate ./my-skill`），**只保留一份**，不要重复。

### 行内代码（`` `…` ``）里的自然语言

- 若 `` `…` `` 里包住的是**用户提问 / prompt 样例 / 自然语言短语**（而不是标识符、命令、文件名、变量名），中文版中要把里面的英文文案翻译成中文，并把 ASCII 引号一并换成中文引号：
  - `` `"Write a fibonacci function"` `` → `` `“写一个斐波那契函数”` ``
  - `` `"analyze this CSV"` `` → `` `“分析这份 CSV”` ``
- 若 `` `…` `` 里是真正的代码/命令/字段名/路径（`SKILL.md`、`user_id`、`WHERE region = 'EMEA'`、`~/data/q4_results.xlsx`），**保持原样**。
- 判断标准：把它当作用户会真的说出口的话吗？是 → 翻译；是代码/标识符 → 不翻译。

### MDX / JSX 组件

- `<Note>...</Note>` → 转成 `>` 引用块。
- `<Card>` / `<CardGroup>` → 剥掉标签，把内部内容按普通 Markdown 处理；若卡片就是一个链接标题 + 描述，转成 `- [Title](/link)\n\n\t描述`。
- `<LogoCarousel />`、`<Tabs>` 等无可翻译文本的自闭合组件保持原样。

### 不翻译的内容

- URL、文件路径、代码/命令、YAML 键名、变量名。
- API/框架/工具专有名词首次可括注中文（如 `frontmatter`（前言）、`progressive disclosure`（渐进式披露）），之后照原词使用。
- `skill` / `SKILL.md` / `agent` 中，`skill` 通常保留原词，`agent` 译作“智能体”。

### 标点符号

- **中文段落里的引号必须用中文全角引号 `“…”`**，不要留 ASCII 的 `"…"`。即使引号里包住的是英文短语或标识符（例如“绝不输出 PII”、“Field not found …”）也用中文引号，因为决定引号形式的是外层语言。
- 单引号同理：中文里用 `‘…’`；但 shell/代码/JSON 字面量里的 `'…'`（如 `WHERE region = 'EMEA'`）保持不变。
- 括号：中文段落里的注释用全角括号 `（…）`；英文缩写就近使用时用半角 `(…)`（如 `progressive disclosure (渐进式披露)`）都可以，按上下文选取，全篇保持一致。
- 顿号 `、` 用于并列词；破折号统一用中文全角破折号 `——`；省略号用 `……`。
- 冒号、分号、句号在中文段落里用中文标点 `：`、`；`、`。`。
- 代码块、内联代码（`` `…` ``）、YAML/JSON/命令示例中的标点**保持原样**，不做全角替换。

## CN file generation rules / 纯中文版生成规则

**生成前先 Read 一次最新的双语文件**，因为用户很可能已经手动修订过。基于双语文件里已有的中文段落（不是重新翻译）来生成 CN 版：

1. **文件名**：`{原名} (CN).md`（`(CN)` 前有一个空格），放在与双语文件相同的目录。
2. **标题**：
   - `# English Title 中文标题` / `# English - 中文` → `# 中文标题`
   - `## English - 中文` → `## 中文`
   - 但对字段/目录类，保留中文侧带的括注：`` #### `name`（名称）字段 ``、`` ### `scripts/` （脚本） ``。
3. **顶部**：保留 `原文地址：...` 一行。
4. **段落 / 列表 / 引用块**：只保留每对里的中文块，删掉英文块。
5. **表格**：只保留中文表格。
6. **代码块**：
   - 双语版里对同一块附了英中两份的，**只保留中文那份**。
   - 只有一份且不含可翻译内容的（纯命令、纯 YAML 键值、frontmatter 示例等），原样保留一份。
7. **不要**引入双语版里不存在的新翻译；如果双语版里某段用户改过措辞，CN 版跟随修订后的版本。

## Terminology quick reference / 术语速查

| English | 中文 |
|---|---|
| Agent | 智能体 |
| Agent Skill / skill | Skill / skill（保留原词） |
| Frontmatter | 前言（Frontmatter） |
| Progressive disclosure | 渐进式披露 |
| Discovery / Activation / Execution | 发现（Discovery）/ 激活（Activation）/ 执行（Execution） |
| Description | 描述 |
| License | 许可证 |
| Compatibility | 兼容性 |
| Metadata | 元数据 |
| Allowed tools | 允许使用的工具 |
| Scripts | 脚本 |
| References | 参考资料 |
| Assets | 静态资源 |

## Existing exemplars / 参考样例

- 双语版：`Others/Agent Skills/Agent Skills Overview.md`、`Others/Agent Skills/Specification.md`、`Others/Agent Skills/For skill creators/Quickstart.md`
- 纯中文版：`Others/Agent Skills/Agent Skills Overview (CN).md`、`Others/Agent Skills/Specification (CN).md`、`Others/Agent Skills/For skill creators/Quickstart (CN).md`

新文件的排版应与上述样例保持一致；如果排版发生冲突，以用户最后一次修订的双语版为准。

## Common mistakes / 常见错误

| 错误 | 正确做法 |
|---|---|
| 逐行插入中文（每个 bullet 后面各跟一条中文） | 整块列表 → 空行 → 整块中文列表 |
| 生成 CN 时重新翻译一遍 | 先 Read 双语版，直接提取中文块 |
| CN 文件里还残留英文段 | 检查是否漏删；只保留中文对应块 |
| 代码块里翻译了 YAML 键或命令本身 | 只翻译注释和字符串文案 |
| 标题只留英文或只留中文（在双语版里） | 双语版标题必须"英文 + 中文"同行 |
| 忘了加 `原文地址：` 一行 | 若已知 URL，加在一级标题下方 |
| `(CN)` 里没有空格，写成 `(CN).md` 紧贴前一个词 | 文件名格式：`{Name} (CN).md` |
| 把本 skill 复制到其他仓库时保留 `bilingual-markdown` 名称 | 换一个名字，例如 `bilingual-md-{project}`，并按需修改术语表 |
| 中文段落里残留 ASCII 引号 `"…"` | 改成中文全角引号 `“…”`；单引号同理改成 `‘…’` |
| 忘了给标题加层级序号 | `##` 加 `1.`、`2.` …，`###` 加 `1.1`、`1.2` …，`#` 不加；双语版和 CN 版编号一致 |
| 把 `` `…` `` 里的英文用户 prompt 当代码保留 | 若引号里是自然语言样例（用户会说出口的话），翻译成中文并改用中文引号；标识符/命令/路径才保持原样 |