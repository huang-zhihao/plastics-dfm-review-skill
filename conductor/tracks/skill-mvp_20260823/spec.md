# 塑件评审 Skill MVP（评审流程骨架 + 七大类核心规则库）

## Overview

交付第一个可用的 ZCode Skill：SKILL.md 定义"高级产品结构工程师（塑料件）"角色与六步评审流程，配套注塑件 DFM 七大类核心规则库，能对一份"设计说明 + 2D 图纸文本描述"输入产出 A/B/C/D 分级意见单。这是全产品的最小闭环。

## Functional Requirements

### FR-1: Skill 骨架与评审流程

SKILL.md 定义：角色（15 年以上塑料件结构经验的高工）、触发条件（用户提供塑料件设计资料要求评审）、六步评审流程（资料接收 → 齐套检查 → 分类逐项审查 → 风险分级 → 意见单输出 → 复审说明）、规则引用纪律。

- Acceptance: 新会话中对"帮我评审这个塑料件设计"能触发，AI 按六步流程执行且不跳步

### FR-2: 七大类核心规则库 v1

类别：壁厚（BT）、脱模斜度（DM）、加强筋（RB）、螺丝柱（BS）、卡扣（SN）、孔与圆角（HL）、缩水与变形风险（SK）。每条规则含：编号、适用条件、推荐值区间、来源标注。

- Acceptance: 规则总数 ≥ 80 条；随机抽查 20 条全部有来源标注与适用条件

### FR-3: 意见单模板与输出

Markdown 意见单：汇总表（等级/数量统计）+ 逐条详情（按 product-guidelines.md 格式）+ 边界声明。

- Acceptance: 对示例输入产出完整意见单；所有意见均引用规则编号，无依据的意见标 D 类

### FR-4: 示例验证案例

编写 1 份含典型错误的示例设计说明（文本），预埋 ≥ 7 个已知问题及标准答案清单，存入 `fixtures/`。

- Acceptance: 全流程试评能检出预埋问题 ≥ 6/7

## Non-Functional Requirements

### NFR-1: 规则库可维护性

Markdown 分文件按类别存放，编号稳定不复用，有索引文件 `references/rules/index.md`。

- Target: 增删改单条规则不影响其他规则编号
- Verification: 抽查索引与文件一致性

### NFR-2: 数值可信性

规则数值全部来自标注来源（塑料件设计手册 / 材料商设计指南 / 国标 / 内部经验，内部经验须标明"经验区间"），SKILL.md 明确写禁止凭记忆给数值。

- Target: 抽查 20 条规则零"无来源"
- Verification: 人工抽查

## Acceptance Criteria

- [ ] Criterion 1: SKILL.md 结构通过 skill-creator 校验，触发可靠
- [ ] Criterion 2: 规则库 ≥ 80 条、七大类齐全、有索引、抽查零无来源
- [ ] Criterion 3: 示例案例评审命中 ≥ 6/7 预埋问题，误报 ≤ 1 条
- [ ] Criterion 4: 意见单格式完全符合 product-guidelines.md

## Scope

### In Scope

- SKILL.md（根目录）
- `references/rules/` 七大类规则文件 + index.md
- `templates/review-report.md` 意见单模板
- `fixtures/case-01/` 示例设计说明 + 预埋问题清单

### Out of Scope

- 材料物性库、公差审查、装配/螺丝选用、卡扣力学计算（Phase 2 track）
- 图纸/截图视觉审查、STEP 解析、docx 报告、复审销项（Phase 3/4 track）
- 独立 subagent 封装

## Dependencies

### Internal

- conductor 上下文已就绪（本 track 即在维护它）

### External

- 无

## Risks and Mitigations

| Risk | Impact | Mitigation |
| --- | --- | --- |
| 规则数值不准导致误报，损害信任 | High | 每条规则标注来源；存疑数值标"经验区间"并提示降为 D 类意见 |
| 范围膨胀（材料/公差被顺手塞进来） | Medium | 严格限定七大类；发现新需求记入 tracks.md Planned 表 |
| 示例案例太简单导致命中率虚高 | Medium | 预埋问题覆盖七个类别，含 1-2 个需要跨类别推理的问题 |

## Open Questions

- [x] 规则库 v1 规模：80 条起步（Phase 2 扩到 120+）
- [ ] 规则来源优先购买/引用哪本手册的数值体系——执行 Task 2.1 时定
