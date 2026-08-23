# Implementation Plan: 塑件评审 Skill MVP

Track ID: `skill-mvp_20260823`
Created: 2026-08-23
Status: completed

## Overview

先立流程骨架（git 仓库、SKILL.md、意见单模板），再分批建规则库，最后用预埋问题的示例案例做全流程验证。按评审反馈扩展 MVP：新增 Top5 材料速查、表面处理/装配公差规则类别、复审销项机制、来源 A/B 分类。

## 扩展交付（按评审反馈并入 MVP）

- [x] **Task 4.1**: 材料速查 `materials.md`（R-MA 6 条：ABS/PC/PC+ABS/PP/PA66 收缩率/壁厚/流动性/耐温 + 材料缺失处理"半盲评"）
- [x] **Task 4.2**: 表面处理 `fn.md`（R-FN 8 条：蚀纹/喷涂/电镀/免喷涂/丝印烫印约束）
- [x] **Task 4.3**: 装配公差 `as.md`（R-AS 8 条：配合间隙/公差累积/定位优先/止口缝隙/热膨胀/MMC/防呆）
- [x] **Task 4.4**: 复审销项机制入 SKILL.md 第 6 步 + 意见单模板第四节销项记录表
- [x] **Task 4.5**: 来源 A/B 分类入 SKILL.md 纪律 1、workflow.md 质量门、rules/index.md 来源约定

## Phase 1: 流程骨架

### Tasks

- [x] **Task 1.1**: `git init` + 目录骨架
  - 根目录建 `SKILL.md`（占位）、`references/rules/`、`templates/`、`fixtures/`
  - 首次提交，`conductor/` 一并入库
- [x] **Task 1.2**: 编写 SKILL.md
  - 角色定义（高级产品结构工程师，塑料件方向）
  - 六步评审流程 + 每步的输入输出
  - 规则引用纪律：意见必须引规则编号、无依据标 D 类、禁止凭记忆给数值
- [x] **Task 1.3**: 意见单模板 `templates/review-report.md`
  - 汇总统计 + 逐条详情格式 + 固定边界声明

### Verification

- [x] **Verify 1.1**: 用 skill-creator 校验 SKILL.md；模拟触发一次"评审请求"，流程六步完整走通（规则库未建时允许输出待补提示）

## Phase 2: 七大类核心规则库

### Tasks

- [x] **Task 2.1**: 壁厚（R-BT）+ 脱模斜度（R-DM）规则
  - 含：常用壁厚区间、厚薄过渡、斜度与表面纹路关系（晒纹加深斜度）
- [x] **Task 2.2**: 加强筋（R-RB）+ 螺丝柱（R-BS）规则
  - 含：筋厚比、筋高、减胶；柱壁厚比、自攻螺丝底孔、爆孔风险
- [x] **Task 2.3**: 卡扣（R-SN）+ 孔与圆角（R-HL）规则
  - 含：卡扣厚度比、进入/导出角；孔间距孔边距、盲孔深径比、内圆角下限
- [x] **Task 2.4**: 缩水与变形风险（R-SK）规则 + 规则索引
  - 含：筋/柱对面外壁缩水判定、壁厚不均变形风险；建 `index.md` 汇总编号

### Verification

- [x] **Verify 2.1**: 规则总数 ≥ 80；随机抽查 20 条，编号规范、有适用条件、有来源，零无来源

## Phase 3: 示例验证与定稿

### Tasks

- [x] **Task 3.1**: 编写示例案例 `fixtures/case-01/`
  - 设计说明文本（一个遥控器外壳之类的简单件）+ 预埋 7 个问题及标准答案
- [x] **Task 3.2**: 全流程试评，统计命中/误报
- [x] **Task 3.3**: 按结果修订规则库与 SKILL.md；更新 product.md 功能状态（F1/F2/F4 → implemented）

### Verification

- [x] **Verify 3.1**: 验收标准全过——命中 7/7、误报 0、判级零偏差；checkpoint 提交并记录 SHA

## Checkpoints

| Phase | Checkpoint SHA | Date | Status |
| --- | --- | --- | --- |
| Phase 1 | f04e8aa | 2026-08-23 | completed |
| Phase 2 | 35567af | 2026-08-23 | completed |
| Phase 3 | 见最终提交 | 2026-08-23 | completed |
