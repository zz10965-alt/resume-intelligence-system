---
name: validate-resume
description: Validate a resume before finalizing: fact support (against Evidence Bank/Registry), cross-section consistency, ATS keyword coverage/parsing, writing quality, and format/length. Use before any resume is considered final, or when the user asks to validate/check a resume.
---

# Validate Resume

对一份简历跑五类校验。任何简历在「final」前必须过这里。

## 五类校验

1. **FACT VALIDATION**：每个重要 claim 回溯 Evidence Bank + Evidence Registry；确认只用 VERIFIED / SAFE_INTERPRETATION。
2. **CONSISTENCY VALIDATION**：检查 company / title / dates / metrics / technology / project identity 全表一致。
3. **ATS VALIDATION**：JD 关键词覆盖、section 命名、解析安全、技能相关性（见 `rules/ATS_RULES.md`）。
4. **WRITING VALIDATION**：语法、清晰度、bullet 强度、重复、冗长（见 `rules/RESUME_WRITING.md`）。
5. **FORMAT VALIDATION**：一页、间距、对齐、字体、溢出、PDF 渲染（见 `rules/FORMAT_RULES.md`）。

## 输出
五类校验逐项 PASS/FAIL + 问题清单 + 建议修改。有 FAIL 则回到 `/generate-resume` 修正。
