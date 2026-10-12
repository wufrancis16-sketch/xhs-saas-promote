# AGENTS.md

本文件是 **Codex / 通用 Agent 的项目级常驻指引**（WorkBuddy 会忽略它，仅用 README.md）。
本仓库是一个 **Agent Skill**：小红书 SaaS 软件推广文案生成器。

## 技能是什么

`SKILL.md` 是技能入口，`references/` 是素材与资料库。技能的作用：输入一个产品方向，产出小红书推广的「标题 + 三段式正文 + 话题标签」，并做去重与合规自检。

## 安装位置

- Codex：把 `xhs-saas-promote/` 放到 `~/.agents/skills/xhs-saas-promote/`（或 `~/.codex/skills/`）
- WorkBuddy：放到 `~/.workbuddy/skills/xhs-saas-promote/`

## 使用约定

当使用者要求生成某个方向的推广内容时：

1. 先读 `references/content-ledger.md` 做去重检测（近 7 天 / 近 30 天）；
2. **严格按产品矩阵调用对应资料**，禁止串用：
   - 业财一体化 / ERP / 项目 ERP / 生产 → `references/product-haoyecai.md`
   - 财务软件 / 会计做账 / 总账报表 / 税务申报 → `references/products.md` 第一部分
   - 代账软件 / 代账公司 → `references/products.md` 第四部分
   - 进销存 / 仓库 / 开单 → `references/products.md` 第二部分
3. 根据 `references/titles.md` 轮换标题类型；
4. 生成后把本次结果（标题 / 方向 / 类型 / 日期 / 话题）追加到 `references/content-ledger.md`。

## 硬性规则（不可违反）

- 标题 ≤20 字（含标点、emoji）；标题类型不得连续重复。
- 三段式结构：痛点（50–80 字）→ 引入软件 → 3–5 个 ✅ 功能点（单独成段）→ 推荐引导（30–50 字）。
- **文案 / 标题 / 话题中不得出现产品真实品牌名**，统一用模糊表达（"这套 ERP""这套财务软件"等）。
- 功能点必须用**对应产品资料里的真实功能名**，不得跨产品串用。
- 违禁词自检：联系方式、平台导流、极限词、收益承诺一律规避。
- 输出只展示「标题 + 正文 + 话题」+（有重复时）台账提示，不输出多余说明。

## 环境提示

- Codex 默认沙箱为 `workspace-write` + 审批，会影响联网与家目录写入。
- 需要联网检索时，在 `~/.codex/config.toml` 开启 `[sandbox_workspace_write] network_access = true`。
- 非交互批量运行可用 `codex exec --full-auto`。
