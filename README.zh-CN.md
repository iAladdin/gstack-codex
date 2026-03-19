# gstack-codex

[English README](README.md)

`gstack-codex` 是一个面向 Codex 的软件工厂，灵感来自 `gstack` 的 workflow 设计，但实现方式完全贴合 Codex：用 trigger-based skills 代替 Claude slash commands，用 `web.run` 做实时资料查询，用本地工具做仓库操作，用持久化 Playwright 浏览器做真实 UI QA。

它提供两层能力：

- 一套 workflow：需求澄清、方案评审、代码审查、根因调查、浏览器 QA、发版、文档同步、复盘
- 一套 browser stack：可持续复用的 `browse` 二进制，用于截图、登录态测试、本地站点验证、staging 回归和多步交互调试

这不是把原项目简单改个名字。Claude 的 slash-command 体系已经被改造成 Codex 技能包，而原项目里最强的实现思路之一，持久化浏览器 daemon，被保留下来了。

## 适合谁

- 想把 AI 开发流程跑顺的创始人和独立开发者
- 想把 review、QA、ship 做得更稳的 tech lead 和 staff engineer
- 不想每次都从空白 prompt 开始的 Codex 用户
- 需要真实浏览器验证，而不是“理论上这个页面应该能用”的团队

## 快速开始

1. 安装到 `~/.codex/skills/gstack-codex`
2. 运行 `./setup`
3. 在任意项目里打开 Codex
4. 从下面任意一句开始：

```text
用 office-hours 帮我把这个产品想法讲清楚：我想做一个能整合日历和邮件的每日简报助手。
```

```text
用 review 审查我当前的改动，先直接给我 findings。
```

```text
用 qa 测试 http://localhost:3000 的登录流程，发现坏掉的地方就直接修掉。
```

## 安装

要求：

- Codex
- Git
- Bun 1.x+
- 如果要导入本机浏览器 Cookie，建议在 macOS 上使用

### 全局安装

```bash
git clone https://github.com/iAladdin/gstack-codex.git ~/.codex/skills/gstack-codex
cd ~/.codex/skills/gstack-codex
./setup
```

`setup` 会：

- 安装依赖
- 构建 `browse/dist/browse`
- 按需安装 Playwright Chromium
- 把子技能注册到 `~/.codex/skills/`

### 直接让 Codex 帮你安装

Codex 可以使用安装在 `~/.codex/skills/` 下的可复用 skills，而这个仓库的结构就是按这个模型组织的。

如果你希望让 Codex 直接从 GitHub 仓库帮你完成安装，可以把下面这段原样发给它：

```text
帮我从 GitHub 安装 gstack-codex。

1. 把 https://github.com/iAladdin/gstack-codex.git clone 到 ~/.codex/skills/gstack-codex
2. 进入那个目录执行 ./setup
3. 检查 ~/.codex/skills/ 下的子技能软链是否已经注册好
4. 确认 browse 可以正常使用
5. 最后告诉我你具体做了哪些改动
```

如果你还想让 Codex 顺手把“当前项目怎么更好地使用这套 skill”也配置一下，可以发这段：

```text
帮我从 GitHub 安装 gstack-codex，并顺手把当前工作区配置得更适合使用它。

1. 把 https://github.com/iAladdin/gstack-codex.git clone 到 ~/.codex/skills/gstack-codex
2. 在那个目录执行 ./setup
3. 检查安装后的 skills 和 browse binary 是否可用
4. 先查看当前仓库，只有在确实能让 skill 使用更清晰的情况下，才新增或更新 AGENTS.md
5. 最后告诉我，这个项目里最推荐怎么调用这套 workflows
```

### 工作仓库和安装副本分离

如果你的真实开发仓库不放在 `~/.codex/skills/gstack-codex`，也没关系。仓库内置了一键同步脚本：

```bash
bin/sync-install
```

它会：

- 把当前工作区同步到 `~/.codex/skills/gstack-codex`
- 排除本地构建产物和运行时目录
- 自动在安装副本里执行 `setup`

也支持自定义目标目录：

```bash
bin/sync-install /some/other/path/gstack-codex
```

## 在 Codex 里怎么调用

这是 Codex 技能包，不是 Claude slash-command 包。

你应该这样写：

```text
用 office-hours 帮我重新梳理一下这个功能。
```

```text
用 plan-eng-review 帮我审一下这个实现方案。
```

```text
用 browse 打开 http://localhost:3000，告诉我页面上有哪些可交互元素。
```

不要这样写：

```text
/office-hours
/qa
/ship
```

## 看它实际工作

```text
你：      用 office-hours 帮我梳理一个给日程准备材料的 AI 助手。

Codex：   先挑战你的原始表述，提炼真实用户痛点，
          看出这其实更像“私人助理 / 幕僚”型工具，
          给出 3 种实现方向，并推荐最窄、最容易验证的一条。

你：      用 plan-ceo-review 接着审这个方向，把第一版范围砍小一点。

Codex：   收缩范围，保留最有学习价值的那一块，
          同时明确指出哪些东西现在先不要做。

你：      用 plan-eng-review 把它整理成可执行的工程方案。

Codex：   把架构、数据流、失败路径、接口边界、
          迁移风险和测试策略都补完整。

你：      用 review 审一下我当前分支的改动。

Codex：   先给 findings，直接指出回归风险和缺失测试。

你：      用 qa 去测 http://localhost:3000，哪坏了就修哪。

Codex：   打开持久化浏览器，走完整流程，检查 console
          和 network，修掉问题后再重新验证一次。

你：      用 ship 帮我确认这版能不能发。

Codex：   跑该跑的检查，把剩余风险讲清楚，
          再整理一份干净的发版摘要。
```

核心思路不是“一个超级长 prompt”，而是一条有节奏的 sprint workflow。

## 这条 Sprint 的结构

`gstack-codex` 围绕下面这个顺序设计：

**Think → Plan → Build → Review → Test → Ship → Reflect**

推荐这样使用：

- `office-hours` 先把问题讲清楚
- `plan-*` 把产品、工程、设计决策逼出来
- `investigate` 先解释 bug，再改代码
- `review` 在合并前抓回归
- `qa` 在真实浏览器里验证真实行为
- `ship` 做发版前的最终把关
- `document-release` 和 `retro` 负责收尾

## Skill 总览

| Skill                   | 角色                        | 功能                                                     | 示例提示词                                                                             |
| ----------------------- | --------------------------- | -------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| `gstack-codex`          | 总路由                      | 当你不确定该从哪个 workflow 开始时，帮你选技能。         | `用 gstack-codex 帮我判断一下，这个任务更适合走 office-hours、plan review 还是 QA。`   |
| `office-hours`          | 需求澄清伙伴                | 把模糊想法重构成真实痛点、隐藏任务和更好的切入点。       | `用 office-hours 帮我梳理这个想法：我想做一个整合日历和邮件的 AI 日报助手。`           |
| `plan-ceo-review`       | Founder / CEO               | 挑战范围、野心、节奏，以及哪些事情现在不该做。           | `用 plan-ceo-review 帮我把这个方案收一收，看看第一版到底该做哪些。`                    |
| `plan-eng-review`       | Engineering lead            | 审架构、接口、数据流、失败路径和测试策略。               | `用 plan-eng-review 审一下这个实现方案，重点看数据流和测试策略。`                      |
| `plan-design-review`    | Design critic               | 在写代码前审视 UX/UI 方案。                              | `用 plan-design-review 看一下这个后台页面方案，重点看层级、清晰度和移动端。`           |
| `design-consultation`   | Design partner              | 产出具体的视觉方向、设计系统和组件规则。                 | `用 design-consultation 帮我给这个 AI 写作产品定一套视觉风格和组件规则。`              |
| `review`                | Staff engineer reviewer     | 对代码和 diff 做 findings-first 审查。                   | `用 review 审查我当前的改动，先直接给我 findings。`                                    |
| `investigate`           | Debugger                    | 先复现、缩小范围、解释 bug 根因，再决定如何修。          | `用 investigate 帮我查一下，为什么用户登录成功后偶尔又会被踢回登录页。`                |
| `design-review`         | Designer who ships          | 审现有页面并直接修掉最重要的设计问题。                   | `用 design-review 看一下 http://localhost:3000/settings，把最明显的设计问题直接修掉。` |
| `qa`                    | QA lead                     | 跑浏览器 QA，修问题，再重新验证。                        | `用 qa 测一下 http://localhost:3000 的注册和登录流程，坏了就修。`                      |
| `qa-only`               | QA reporter                 | 同样深度的 QA，但只出报告不改代码。                      | `用 qa-only 测一下 staging 上的下单流程，只给我 bug 报告，不要改代码。`                |
| `ship`                  | Release engineer            | 做发版前检查、测试和交付收尾。                           | `用 ship 帮我确认当前分支能不能发。`                                                   |
| `document-release`      | Technical writer            | 更新 README、setup、运行说明等文档，使其和最新行为一致。 | `用 document-release 把最近这次登录改动涉及到的 README 和部署说明更新一下。`           |
| `retro`                 | Engineering manager         | 复盘这次迭代做了什么、哪里出问题、下次怎么改。           | `用 retro 帮我复盘这次迭代，重点说说测试和流程上暴露的问题。`                          |
| `browse`                | Persistent browser operator | 打开真实页面、截图、走登录态、多步点击、检查浏览器状态。 | `用 browse 打开 http://localhost:3000，告诉我有哪些可交互元素，再顺手截个图。`         |
| `setup-browser-cookies` | Session manager             | 导入本机 Chromium 系浏览器里的登录态 Cookie。            | `用 setup-browser-cookies 把 Chrome 里 app.example.com 的登录态导到 browse 里。`       |
| `codex`                 | Second-opinion reviewer     | 显式触发独立的第二意见或 challenge workflow。            | `用 codex 对我当前的 diff 做一次第二意见 review，重点挑战边界情况。`                   |
| `careful`               | Safety mode                 | 在高风险操作前明确 blast radius 和 rollback。            | `用 careful 帮我处理这次生产库变更，任何危险操作前都先跟我确认。`                      |
| `freeze`                | Scope lock                  | 把本次修改限制在一个目录或模块内。                       | `用 freeze，把这次改动范围限制在 apps/web/src/settings。`                              |
| `guard`                 | Safety + scope lock         | 组合 `careful` 和 `freeze`。                             | `用 guard 处理这个支付问题，只允许改 payments 模块，而且危险命令都要先确认。`          |
| `unfreeze`              | Scope unlock                | 解除当前的修改范围限制。                                 | `用 unfreeze，把刚才的改动范围限制取消掉。`                                            |

## 浏览器层为什么重要

这个仓库里最硬核的实现，其实是 `browse` 这一层。

它解决的是：

- 本地项目 `http://localhost:3000` 可以真实测试
- 登录后页面可以真实测试
- 多步 UI 流程可以真实测试
- 截图、console、network 证据很容易拿到
- 浏览器常驻，不需要每次冷启动

典型用法：

```text
用 browse 打开 http://localhost:3000，告诉我页面上有哪些可交互元素。
```

```text
用 qa 测试 http://localhost:3000 的登录流程，发现问题就修掉。
```

```text
用 setup-browser-cookies 把 Chrome 里 staging.example.com 的登录态导进来。
```

## 和原版 gstack 的差异

- 不再使用 Claude slash commands
- 不再依赖 Claude 专属的 `AskUserQuestion` 和 `CLAUDE.md` 机制
- 公网上的信息查询优先走 `web.run`，真实交互和本地页面走 `browse`
- `codex` 不再默认包装外部 Codex CLI，而是 Codex 内部的“独立第二意见” workflow
- `careful`、`freeze`、`guard`、`unfreeze` 现在更偏向 Codex 当前任务范围，而不是长期 Claude 会话状态

## 仓库结构

| 路径               | 作用                         |
| ------------------ | ---------------------------- |
| `SKILL.md`         | 整个技能包的总路由技能       |
| `references/`      | 共享原则和 playbook          |
| `<skill>/SKILL.md` | 每个 workflow 一个技能       |
| `browse/`          | 持久化 Playwright 浏览器实现 |
| `bin/`             | setup、sync 和辅助脚本       |
| `BROWSER.md`       | 浏览器命令参考和实现说明     |

## 开发

```bash
bun install
bun run build
```

浏览器运行时状态默认会写到当前项目根目录下的 `.gstack-codex/`。

## 故障排查

**技能没显示出来？**

```bash
cd ~/.codex/skills/gstack-codex
./setup
```

**本地改完代码后想刷新安装副本？**

```bash
bin/sync-install
```

**`browse` 不可用？**

```bash
~/.codex/skills/gstack-codex/browse/bin/find-browse
```

如果找不到，再执行：

```bash
cd ~/.codex/skills/gstack-codex
./setup
```

## License

MIT.
