# xhs-saas-promote

小红书 **SaaS 软件推广文案**生成技能（Agent Skill / SKILL.md 开放标准）。

输入一个产品方向（财务软件 / 进销存 / ERP / 代账软件 / AI 财务 / 项目 ERP……），自动产出**小红书平台调性**的推广内容：

- 一个 ≤20 字的标题（按 6 种标题类型轮换）
- 一篇三段式正文（痛点场景 → 功能解决方案 → 推荐引导）
- 3–5 个话题标签

并内置一整套**防同质化 / 防违规**机制：内容台账去重、标题类型轮换、违禁词自检、零品牌名规范、产品矩阵严格对应。

---

## 宿主支持（WorkBuddy + Codex 双宿主）

| 项目 | WorkBuddy | Codex CLI |
|------|-----------|-----------|
| 用户级技能目录 | `~/.workbuddy/skills/xhs-saas-promote/` | `~/.agents/skills/xhs-saas-promote/`（官方 USER 位置）或 `~/.codex/skills/` |
| 仓库级技能目录 | `<repo>/.workbuddy/skills/xhs-saas-promote/` | `<repo>/.agents/skills/xhs-saas-promote/` |
| 唤起方式 | 输入 `/xhs-saas-promote` 或 `@skill:xhs-saas-promote` | 先 `/skills` 列出，再 `$xhs-saas-promote <prompt>` |
| 项目级常驻指引 | 本 `README.md` | 同仓库的 `AGENTS.md` |
| 执行环境 | 有文件读写 + 可联网 | 默认沙箱 `workspace-write` + 审批，联网需在 `~/.codex/config.toml` 开 `[sandbox_workspace_write] network_access = true`；非交互跑批用 `codex exec --full-auto` |

> 技能文件名固定为 `SKILL.md`（跨 Agent 开放标准），`name` + `description` frontmatter 两端都读。
> 技能内部**不写死绝对路径**，迁移到任一宿主目录均可直接使用。

---

## 目录结构

```
xhs-saas-promote/
├── SKILL.md                  # 技能主文件：规范、格式、流程、标题/话术规则
└── references/               # 素材与资料库
    ├── products.md           # 产品矩阵资料（好会计 / 好生意 / 好业财 / 易代账）
    ├── product-haoyecai.md   # 好业财（业财一体化 ERP）专项资料
    ├── features.md           # 通用功能点素材库
    ├── scenes.md             # 痛点场景素材库
    ├── titles.md             # 6 种标题类型示例库
    ├── competitors.md        # 竞品对比素材（仅用户点名单机版时调用）
    ├── history.md            # 历史发布记录
    ├── writing-framework.md  # 文案框架规范
    └── content-ledger.md     # 内容台账（发布去重用，生成后自动追加）
```

---

## 使用方法

1. 把整个 `xhs-saas-promote/` 目录放到宿主的技能目录下（见上表）；
2. 在对话中唤起技能，直接说明方向即可，例如：
   - 「帮我写一篇进销存仓库管理开单软件方面的内容」
   - 「帮我写一篇 AI 财务软件的内容」
   - 「帮我写一篇项目型公司 ERP 的内容，功能全一些」
3. 技能会：读台账去重 → 调用对应产品资料取真实功能名 → 按标题类型轮换生成 → 输出「标题 + 正文 + 话题」→ 自动追加台账。

---

## 规范要点（核心）

- **标题 ≤20 字**（含标点、emoji），6 种类型轮换，不连续重复同一风格
- **三段式**：第一段痛点 50–80 字；第二段引入 + 3–5 个 ✅ 功能点（单独成段）；第三段推荐引导 30–50 字
- **零品牌名**：正文 / 标题 / 话题中不得出现产品真实品牌名，一律用「这套 ERP」「这套财务软件」等模糊表达；**调用产品资料是为了取真实功能名与差异化卖点，不是为了写品牌名**
- **产品矩阵严格对应**：财务软件 → 好会计；进销存 → 好生意；代账 → 易代账；业财一体 / ERP / 项目 → 好业财。**严禁串用**（如「财务软件」绝不能调用好业财 ERP 的功能）
- **违禁词自检**：联系方式、平台导流、极限词、收益承诺等一律替换或规避
- **台账去重**：生成前读 `content-ledger.md`，对方向 / 类型 / 话题做重复检测并给出警告

---

## 说明

本仓库为推广内容生产工具，`references/` 内含产品资料与历史发布台账，仅供内部协作使用。
