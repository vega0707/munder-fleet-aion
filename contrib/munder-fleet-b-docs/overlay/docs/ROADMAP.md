# ROADMAP — Strategy B

## P0
- [x] 抽出 `fleet-daemon` 无头进程（行为 ≈ 现 Electron main 的 hive/pty）
- [x] `fleet-gateway`：密码/令牌 session + Local 身份免鉴权（非 IP 旁路）
- [x] PendingDecision 硬闸
- [x] Runtime.ensureLocal()

## P1
- [x] TeamWake + 完成回传 Michael（对齐 Aion internals 时序）
- [x] Web：看板（assignee）+ 待定列表 + 角色注册 UI

## P2
- [x] 多机 runtime + claim（手动/自动 `AutoClaimLoop`）
- [x] Blocker → owner
- [x] 契约测试对拍 Multica 生命周期

## P3
- [x] 穿透文档、观测、从 A/C 策略吸收教训（`docs/OPS.md` + `/metrics` + CI）

## P4 — 对标 WorkBuddy + 吸收 EvoX（见设计方向）

依据 [`docs/DESIGN_DIRECTION.md`](./DESIGN_DIRECTION.md) · [`docs/WORKBUDDY_ANALYSIS.md`](./WORKBUDDY_ANALYSIS.md)：在 P0–P3 Fleet 语义面之上，补 Expert/Skill/Project 与**程序汇合**纪律；**不改变单一 Fleet 协议**。

### P4-a（类型与格式 · WorkBuddy）
- [ ] Expert 模型：Role 扩展为「定位 + 方法论 + 默认 Skill/Connector」（`fleet-protocol`）
- [ ] Skill 包格式：`SKILL.md` + 脚本 + 工具白名单；Project 级预置（`fleet-daemon` loader）
- [ ] Project 配置中心：全局指令、默认 Expert/Skill、连接器注入新 Task（gateway + shell-web）

### P4-b（编排与汇合 · EvoX 纪律）
- [ ] SubTask / 等价子 claim：单 Task 内多 Role 并行
- [ ] 结构化 complete payload（`subtaskId` + 字段/产物引用）
- [ ] **程序 merge**（按编号拼接/模板装配）；Michael **默认禁止** LLM 转述重写终稿
- [ ] 产物交付区：版本化、可检查、可迭代（非仅 stdout）
- [ ] 契约测试：子块保留率（防「汇总丢答案」回归）

### P4-c（经验与企业）
- [ ] Experience 轻量沉淀（成功路径可追溯注入；组织内，非公网市场）
- [ ] Memory：跨 Task 个人偏好（与 Project 团队标准分离）
- [ ] Connector：MCP + 可选 IM/文档
- [ ] 企业治理（模块化借 A）：SSO、审计、用量——不 fork 整仓 A

### P4 非目标
- 公有云代跑 agent 算力（与 P0–P3 一致）
- 内置 100+ 办公 Expert **内容库**（属内容与运营，非本仓 P4 工程范围）
- 默认「Lead LLM 汇总子 Agent」的 Sub-Agent 产品形态
- Multica Go 主核或 AionUi 替换 Munder 壳
