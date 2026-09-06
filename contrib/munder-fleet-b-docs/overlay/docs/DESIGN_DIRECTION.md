# 设计方向 — Strategy B（对标 WorkBuddy + 吸收 EvoX）

> 决策日期：2026-09-06  
> 状态：**已拍板方向**（产品主路径 = B；P4 起叠产品层）  
> 依据：[`WORKBUDDY_ANALYSIS.md`](./WORKBUDDY_ANALYSIS.md) · EvoX/EvoMap 蜂群协作公开评测（[微信文](https://mp.weixin.qq.com/s/BrhHRQRJe52nFJm7_wmzEw)）  
> 落地清单：[`ROADMAP.md`](./ROADMAP.md) § P4

---

## 1. 一句话方向

**以 Strategy B（Munder TS monorepo）做产品主路径**：在已落地的 Fleet 语义面（claim / Runtime / PendingDecision / Michael）之上，叠 **WorkBuddy 式 Expert·Skill·Project 产品层**，并吸收 **EvoX 式「程序汇合、禁止 Lead LLM 转述」+ 经验沉淀**，最终形成「可接活的办公楼 Agent 工作台」。

不换成 AionCore 主核（A）、不推倒重写协议（C）、不以 Multica 作商用主核（D）。

---

## 2. 外部参照怎么用

三层参照，**叠用而非三选一**：

| 参照 | 我们取什么 | 我们不取什么 |
|------|------------|--------------|
| **WorkBuddy** | Expert / SkillHub / Project 团队标准注入 / 产物交付区 / 企业治理叙事 | 腾讯文档生态锁死；用「团长 LLM 重写汇总」当默认汇合 |
| **EvoX / EvoMap** | 子结果 **按 subtaskId 程序 merge**；跑通路径沉淀为可复用经验（AI for AI） | 做成纯研究蜂群、丢掉 assignee 看板与真人硬闸 |
| **Multica（语义）** | Runtime 注册 / heartbeat / claim / blocker→owner | 整仓 Go 主核、对外 SaaS vendor |
| **Aion（模块）** | auth 合同、TeamWake→Michael、远期 SSO/审计 | 整仓 Rust 替换 TS 主栈；AionUi 换皮 |

```
WorkBuddy 产品层          EvoX 编排纪律
 Expert · Skill · Project   程序汇合 · 经验复用
            \               /
             \             /
              ▼           ▼
        Strategy B 主路径（本仓）
     Fleet 语义 + Munder 壳 + TS daemon
              ▲
              │ 模块化借
         Aion auth / wake · Multica claim 语义
```

---

## 3. 目标产品形态（B 终点图像）

用户侧一句话：**在 Munder 办公楼里派活；专家/角色按 Project 标准接活；结果按块交卷，可检查、可迭代；疑难进硬闸。**

### 3.1 核心对象（统一，无第二套）

| 对象 | 方向定义 |
|------|----------|
| `Project` | **团队标准注入器**：全局指令、默认 Expert/Skill、Connector、资料边界；新建 Task 自动注入 |
| `Task` | 一次可迭代执行链；`assignee` 权威「谁做」；状态 `todo\|doing\|blocked\|done` |
| `Expert` | Role 的产品化：定位 + 方法论 + 默认 Skill/工具白名单（≠ 仅 UI 头像） |
| `Skill` | `SKILL.md` + 脚本/模板 + 工具白名单；Project 可预置；可版本化 |
| `Runtime` | `daemon × 已装 CLI`；本机 `ensureLocal`；多机同协议 claim |
| `PendingDecision` | 硬闸；`ownerId` 决定谁解；未解不得继续工具路径 |
| `Michael` | 编排与收件；**默认不做「读齐子结果再 LLM 重写」** |
| `Artifact` | Task 产物块（文件/报告片段）；按 `subtaskId` 可拼接、可验收 |
| `Experience`（P4+） | 跑通路径的机器可读摘要；供后续 Task/Expert 复用（对齐 EvoMap，不做公有经验市场一期） |

### 3.2 汇合纪律（吸收 EvoX，写进协议）

1. 复杂 Task 可拆 `SubTask`（或等价子 claim）；各 Runtime/Expert **并行**。
2. 完成回传必须是 **结构化 payload**（`subtaskId` + 约定字段/产物引用），**禁止**仅一段自由文本摘要作为唯一结果。
3. **Merge = 程序按编号/字段拼接**（或固定模板装配）；Michael / Lead **默认不得**再经 LLM「理解一遍重写终稿」。
4. 允许的 LLM 后处理仅限：**显式用户请求**的润色/排版，或 **独立质检 Expert** 输出「质检意见」附件——不替换原始块。
5. 子结果已正确、终稿却错 —— 视为汇合层回归；契约测试应覆盖「子块保留率」。

### 3.3 经验纪律（AI for AI，轻量起步）

1. Skill = 人预置的能力包；Experience = **跑通后沉淀**的可复用痕迹（成功步骤、关键约束、失败原因）。
2. 新 Task 在同 Project 内可检索相关 Experience；注入须可追溯（哪条经验、何时）。
3. 一期不做公网经验市场；仅本机/组织内。

---

## 4. 为何主路径是 B（相对 A/C/D）

| 策略 | 结论 |
|------|------|
| **B** | **主路径**。单 TS 栈 + 完整 Munder 壳，叠 Expert/Skill/Project/汇合纪律最快；P0–P3 Fleet 已落地。 |
| **A** | **模块供应商**。借 auth / TeamWake / 远期 SSO；不整仓换 Rust 主后端（否则产品层迭代被双栈拖死）。 |
| **C** | **长期洁癖备选**。PROTOCOL 可把「禁止 LLM 转述」写死；到 WorkBuddy+EvoX 水位最慢，不作追赶主路径。 |
| **D** | **语义参考，不作商用主核**。claim 开箱好，但许可限制 SaaS；场景偏 dev fleet，非办公 Expert/产物。 |

硬约束（不变）：

- 单一 Fleet 协议；禁止 `solo|distributed`
- 表现层品牌 **Munder**
- Multica **协议重写**，不 vendor 源码做对外 SaaS

---

## 5. 分层架构（目标态）

```
┌──────────────────────────────────────────────────────────┐
│ Munder Shell（Electron Local / Web 鉴权）                 │
│ 办公楼 · assignee 看板 · Project 配置 · 产物区 · 待定列表  │
└──────────────────────────┬───────────────────────────────┘
                           │ HTTP/WS
┌──────────────────────────▼───────────────────────────────┐
│ fleet-gateway                                            │
│ identity local|userSession · CSRF ·（远期 SSO 借 A）      │
└──────────────────────────┬───────────────────────────────┘
                           │
┌──────────────────────────▼───────────────────────────────┐
│ fleet-daemon                                             │
│ RuntimeRegistry · Claim · DecisionGate · TeamWake        │
│ Expert/Skill loader · SubTask 程序 merge · Experience    │
│ Michael inbox（收件 ≠ LLM 终稿改写）                      │
└──────────────────────────┬───────────────────────────────┘
                           │ pty / CLI
┌──────────────────────────▼───────────────────────────────┐
│ Local Agent CLIs（Claude / Codex / Cursor / …）          │
└──────────────────────────────────────────────────────────┘
```

---

## 6. 里程碑对齐（只定方向，细项见 ROADMAP）

| 阶段 | 方向重点 |
|------|----------|
| **已完成 P0–P3** | Fleet 单节点→多机语义、硬闸、Wake、观测 |
| **P4-a** | Expert 模型 + Skill 包格式 + Project 配置注入 |
| **P4-b** | SubTask 结构化完成 + **程序 merge**（EvoX 纪律）+ 产物区 |
| **P4-c** | Experience 轻量沉淀；Connector/IM 按需；企业治理模块化借 A |

非目标（本方向明确不做）：

- 公有云代跑 agent 算力
- 100+ 办公 Expert **内容运营库**（工程只留格式与安装器）
- Multica Go 主核 / AionUi 替换壳
- 默认「Lead LLM 汇总子 Agent 答案」的 Sub-Agent 产品形态

---

## 7. 成功判据（方向级）

1. **主路径清晰**：对外与对内文档均指向 B；A/C/D 角色如上表，无双主核。
2. **产品层可演**：至少 1 个 Project 能预置 Expert+Skill，并注入新 Task。
3. **汇合不丢块**：并行子任务完成后，终稿字段/产物能追溯到各 `subtaskId`，且无默认 LLM 重写路径。
4. **硬闸仍在**：PendingDecision 未解时工具路径硬失败（与 P0–P3 一致）。
5. **品牌与协议**：Munder 壳 + 单一 Fleet；本地仍是单节点拓扑。

---

## 8. 决策摘要

| 问题 | 决定 |
|------|------|
| 产品主仓？ | **munder-fleet-b（Strategy B）** |
| 对标谁？ | WorkBuddy（产品层）+ EvoX（汇合/经验纪律） |
| A/C/D？ | A 模块借、C 备选、D 仅语义 |
| Michael 是否汇总改写？ | **默认否**；程序 merge |
| 下一步工程？ | 执行 ROADMAP § P4（先 Expert/Skill/Project，再结构化 merge） |
