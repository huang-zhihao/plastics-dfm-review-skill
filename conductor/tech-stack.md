# Tech Stack

## 形态与运行环境

| Technology | Version | Purpose |
|---|---|---|
| ZCode Skill 规范 | - | SKILL.md + references/ + templates/ + fixtures/ 目录结构 |
| Markdown | - | 规则库、检查清单、意见单模板（版本可控、LLM 友好、无依赖） |

## 配套工具（已安装）

| Tool | Purpose | Notes |
|---|---|---|
| skill-creator | Skill 的创建、校验与迭代维护 | SKILL.md 定稿前必须过一遍校验 |
| document-skills (docx) | 正式评审报告输出 | Phase 3 接入 |
| vision-helper | 2D 图纸、3D 截图的视觉审查 | Phase 4 接入，主模型看不到图时走 vision-helper 子 agent |

## 进阶（Phase 4 评估后再引入）

| Technology | Purpose | Notes |
|---|---|---|
| Python 3.12 + CadQuery | STEP 模型解析，壁厚/拔模角/筋厚自动测量 | 能脚本化的规则从"语义审查"升级为"数值核查" |

## 基础设施

- **无服务器、无数据库**：MVP 全部为本地 Markdown 文件，git 管理
- 仓库根目录即 skill 源码目录（SKILL.md 在根目录），`conductor/` 为项目管理目录，互不干扰
- 部署方式：将 skill 目录复制/链接到 `C:\Users\ASUS\.zcode\skills\`（或打包分享给同事）
- 规则库组织：`references/rules/` 按类别分文件，规则编号格式 `R-{类别码}-{序号}`（如 R-BT-03 = 壁厚类第 3 条）
