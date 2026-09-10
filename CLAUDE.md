# Resume Intelligence System

> 长期、可维护、基于真实证据的求职简历系统。本文件是 Claude Code 的项目操作手册（自动加载）。

## ⚠️ 开始前必读（不可跳过）

开始**任何任务**（尤其「生成 / 改写简历」）前，必须先**读完所有文件、仔细读**，读完之前**不得开始写**：

1. `rules/` 下全部规则文件（FACT_RULES、VARIANT_CONSISTENCY、FORMAT_PRESERVATION、RESUME_WRITING、ATS_RULES、FORMAT_RULES、MARKET_RULES、ROLE_CLASSIFICATION、CN_RESUME_STANDARD）
2. `.claude/skills/` 下全部 SKILL.md
3. `source/experience_bank/` 全部内容（internships、projects、education.md、skills.md）
4. `source/evidence_registry/registry.yaml`
5. `source/inbox/` 下**所有**原始材料（中英简历、实习报告、项目 PDF、论文、成绩单、课程作业等，全部读，不只任务相关）

## 一句话定位

以 **Source of Truth（经历库）** 为唯一事实来源，按「中美市场 × 目标方向」生成**真实、可追溯、跨版本一致**的定向简历，导出可编辑 DOCX + 最终 PDF + Match Report。

## 最高原则（不可违背）

1. **真实性 > ATS 关键词命中**：任何 Target Resume 不能脱离 Source of Truth 独立产生事实。
2. **证据可追溯**：每个重要事实要能回溯到 source file（含 page/sheet/cell 等）。
3. **跨版本一致（硬约束）**：ONE CORE CAREER STORY + SMALL CORE PROJECT BANK（3–4 个）+ 每份简历约 2 个同项目，仅改定位/措辞，不改事实。详见 `rules/VARIANT_CONSISTENCY.md`。
4. **中美市场分离**：中国与美国市场分析、JD、简历变体完全分开。
5. **Raw Evidence 永保**：generated content 绝不覆盖原始证据。
6. **原始简历格式保留（硬约束）**：照片、个人信息、Section 顺序不动，只改内容；字体/行距可微调以保持一页。详见 `rules/FORMAT_PRESERVATION.md`。

## 数据流水线

```
RAW EVIDENCE → INGESTION → SOURCE OF TRUTH / EXPERIENCE BANK → MASTER RESUME
→ MARKET PROFILES → BASE VARIANTS → TARGET JD 分析 → JD↔EVIDENCE 匹配
→ 定向生成 → FACT/ATS/FORMAT 校验 → DOCX + PDF + MATCH REPORT
```

## 证据状态（Evidence Status）

| 状态 | 含义 | 能否自动进简历 |
|---|---|---|
| `VERIFIED` | 原始材料明确支持 | ✅ 自动可用 |
| `SAFE_INTERPRETATION` | 合理总结、不改事实 | ✅ 自动可用 |
| `UNVERIFIED` | 只有记忆/旧简历，缺证据 | ❌ 需补证据 |
| `CONFLICT` | 多源冲突 | ❌ 需用户确认 |
| `DO_NOT_CLAIM` | 没做过 / 不能证明 | ❌ 永不写入 |

> 定向简历默认只能自动使用 `VERIFIED` 与 `SAFE_INTERPRETATION`。

## 规则文件索引

| 文件 | 内容 |
|---|---|
| `rules/FACT_RULES.md` | 证据状态、真实性红线、provenance 规范 |
| `rules/VARIANT_CONSISTENCY.md` | 跨版本经历/项目一致性（硬约束） |
| `rules/ROLE_CLASSIFICATION.md` | DA / BA / DS / AI Analytics / Specialized 分类规则 |
| `rules/RESUME_WRITING.md` | bullet 写法、措辞规范 |
| `rules/ATS_RULES.md` | ATS 关键词、section 命名、解析安全 |
| `rules/FORMAT_RULES.md` | 一页、排版、字体、边距 |
| `rules/FORMAT_PRESERVATION.md` | 原始简历格式保留（照片/个人信息/section 顺序不动，只改内容，字体行距可微调） |
| `rules/MARKET_RULES.md` | 市场分析、JD 加权与去重 |
| `rules/CN_RESUME_STANDARD.md` | 中文简历标准模板（以 DA 终版为准：字体/字号/结构/bullet 写法，所有中文变体照此） |

## Skills（工作流入口，位于 `.claude/skills/`）

| Skill | 作用 |
|---|---|
| `/ingest-evidence` | 摄入新原始文件 → 更新 Registry + Experience Bank + 冲突报告 |
| `/analyze-jd` | 单个 JD 分类、关键词、匹配、推荐 Base |
| `/analyze-market` | 基于 JD 库生成/更新某市场画像 |
| `/generate-resume` | 目标 JD → 定向简历源 |
| `/validate-resume` | 事实 / 一致性 / ATS / 写作 / 格式 校验 |
| `/compare-resume` | Base vs Target 差异解释 |
| `/export-resume` | MD → DOCX → PDF + Match Report |

## 目录结构（关键）

- `source/raw/` = 原始证据（只增不改）
- `source/inbox/` = 新文件投放处
- `source/experience_bank/` = Source of Truth（经历库；项目含 `source_of_truth.md` + 各角色 representation）
- `source/evidence_registry/` = fact → source 追溯
- `jd/` = JD 库（raw / china / us / processed）
- `market_profiles/` = 中美市场画像
- `resume/` = master / base_variants / templates
- `rules/` = 系统规则
- `output/` = 生成产物（不覆盖证据）
- `archive/` = 历史版本

## 当前阶段

**Phase 1 —— 系统初始化**：搭框架 + 规则 + 技能。**尚未生成最终简历**，等用户批准后再进入批量生成。
