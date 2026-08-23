# 塑件评审 Skill MVP（评审流程骨架 + 九大规则类别 + 材料速查）

## Overview

交付第一个可用的 ZCode Skill：SKILL.md 定义"高级产品结构工程师（塑料件）"角色与六步评审流程（含复审销项闭环），配套注塑件 DFM 九大规则类别（壁厚/脱模斜度/加强筋/螺丝柱/卡扣/孔与圆角/缩水变形/表面处理/装配公差）+ Top5 材料速查，能对一份"设计说明 + 2D 图纸文本描述"输入产出 A/B/C/D 分级意见单，并支持修改后逐条销项复核。这是全产品的最小闭环。

## Functional Requirements

### FR-1: Skill 骨架与评审流程

SKILL.md 定义：角色（15 年以上塑料件结构经验的高工）、触发条件（用户提供塑料件设计资料要求评审）、六步评审流程（资料接收 → 齐套检查 → 分类逐项审查 → 风险分级 → 意见单输出 → 复审说明）、规则引用纪律。

- Acceptance: 新会话中对"帮我评审这个塑料件设计"能触发，AI 按六步流程执行且不跳步

### FR-2: 九大规则类别 + 材料速查 v1

类别：壁厚（BT）、脱模斜度（DM）、加强筋（RB）、螺丝柱（BS）、卡扣（SN）、孔与圆角（HL）、缩水与变形风险（SK）、表面处理（FN）、装配公差（AS），另加 Top5 材料速查（MA：ABS/PC/PC+ABS/PP/PA66 收缩率/推荐壁厚/流动性/耐温）。每条规则含：编号、适用条件、推荐值区间、来源标注（A 类=标准/datasheet/手册；B 类=行业经验值）。

- Acceptance: 规则总数 ≥ 100 条；A 类来源占比 ≥60%；随机抽查 20 条全部有适用条件与来源标注，无裸数值

### FR-3: 意见单模板与输出

Markdown 意见单：汇总表（等级/数量统计）+ 逐条详情（按 product-guidelines.md 格式）+ 边界声明。

- Acceptance: 对示例输入产出完整意见单；所有意见均引用规则编号，无依据的意见标 D 类

### FR-4: 示例验证案例

编写 1 份含典型错误的示例设计说明（文本），预埋 ≥ 7 个已知问题及标准答案清单，存入 `fixtures/`。

- Acceptance: 全流程试评能检出预埋问题 ≥ 6/7

### FR-5: 复审销项机制

收到修改后版本时，调出上一轮意见单逐条复核，标记每条意见状态：已修复 / 未修复 / 仍有问题，输出销项记录表（模板第四节）；未销项意见自动带入下一轮，A/B 级未销项在意见单顶部醒目提示。

- Acceptance: 对修改版输入能输出销项记录表；A/B 级未销项意见被醒目列出

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
- [ ] Criterion 2: 规则库 ≥ 100 条、九大类别 + 材料速查齐全、有索引、A 类占比 ≥60% 且无裸数值
- [ ] Criterion 3: 示例案例评审命中 ≥ 6/7 预埋问题，误报 ≤ 1 条
- [ ] Criterion 4: 意见单格式完全符合 product-guidelines.md

## Scope

### In Scope

- SKILL.md（根目录）
- `references/rules/` 九大类别规则文件 + 材料速查 + index.md
- `templates/review-report.md` 意见单模板（含销项记录表）
- `fixtures/case-01/` 示例设计说明 + 预埋问题清单 + 试评输出

### Out of Scope

- 完整材料物性库（Top5 已前置，全材料库 Phase 2）、公差审查深化、卡扣力学计算（Phase 2 track）
- 图纸/截图视觉审查、STEP 解析、docx 报告（Phase 3/4 track）
- 真实用户验证（Phase 3 独立 track：`user-validation`）
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
