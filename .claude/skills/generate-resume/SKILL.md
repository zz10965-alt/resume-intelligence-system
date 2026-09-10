---
name: generate-resume
description: Generate a targeted resume for a specific JD by selecting a base resume, retrieving matching evidence, mapping JD requirements to evidence, optimizing bullet selection/ordering/wording, and producing the resume source. Use when the user asks to "generate a resume for this JD".
---

# Generate Resume

目标 JD → 定向简历源（Markdown）。**事实只能来自 Source of Truth。**

## 前置规则（必读）
- `rules/VARIANT_CONSISTENCY.md`（跨版本一致：实习全一致；项目 2–3 个按方向选最适配、保持部分重叠）
- `rules/FACT_RULES.md`（只用 VERIFIED / SAFE_INTERPRETATION；沾边就写）
- `rules/FORMAT_PRESERVATION.md`（保留原简历格式：照片/个人信息/section 顺序不动，只改内容）
- `rules/RESUME_WRITING.md`（bullet 写法、自然语言、量化）
- `rules/ATS_RULES.md`（关键词在真实前提下融入）

**JD 关键词来源**：优先读对应市场画像 `market_profiles/china/CN_XX.md` 的「Keywords worth including / NOT worth overfitting」字段（该字段来自 `jd/china/中国JD search.xlsx` 对应 sheet）；若该方向无画像，才直接解析 JD。

## 步骤

1. **Parse JD**：market、role family、seniority、industry、职责、required/preferred skills、ATS keywords。
2. **选 Base**：CN_DA/CN_BA/CN_DS/CN_AI_Analytics/US_DA/US_BA/US_DS 之一。
3. **证据检索**：从 Experience Bank 找最相关 VERIFIED/SAFE_INTERPRETATION 事实。
4. **JD↔Evidence 映射**：逐条映射；无证据 → 记 GAP，**不编造**。
5. **优化**：Skills 顺序、bullet 选择/顺序、项目选择/顺序、措辞、ATS 关键词位置（真实性优先）。
6. **项目选择**：默认用核心项目库中的 DEFAULT 2 个项目；换项目需满足 VARIANT_CONSISTENCY.md 的切换阈值，并在 Match Report 解释。
7. **生成**：产出 `output/targeted/<Candidate_Role_Company>.md`。
8. **校验**：调 `/validate-resume`。
9. **匹配报告**：生成 `_match_report.md`（见 generate 输出规范）。

## 输出
简历 Markdown 源 + Match Report + 变更说明。**不直接导出 DOCX/PDF**（交给 `/export-resume`）。
