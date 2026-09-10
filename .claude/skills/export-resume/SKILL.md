---
name: export-resume
description: Export a resume Markdown source to DOCX (editable) and PDF (final), plus generate the match report, following the MD→DOCX→PDF pipeline. Use when the user asks to export, produce DOCX/PDF, or finalize a resume.
---

# Export Resume

把已校验通过的简历 Markdown 源，导出为 DOCX + PDF + Match Report。

## 前置
- 先跑 `/validate-resume` 通过。
- `rules/FORMAT_RULES.md`（一页、排版、中英兼容、ATS 友好）。
- `rules/FORMAT_PRESERVATION.md`（**硬约束**：保留照片/个人信息/section 顺序，只改内容，字体行距可微调，bullet 排满行）。

## 管线
```
Markdown（规范源）
   → DOCX（人工可编辑交付物）
   → PDF（最终投递交付物）
```

## 步骤

1. 确认 Markdown 源已过校验。
2. **若存在用户原始格式简历（DOCX）**：以其为格式母版，用 python-docx 原地替换文本，保留照片/个人信息/section 顺序（见 FORMAT_PRESERVATION.md）。**不要**从 Markdown 重新生成 DOCX。
3. 若无原始格式简历：才走 Markdown → DOCX 生成。
4. 生成 PDF。
4. **视觉校验 PDF**：一页、无溢出/裁切、边距/间距/字体一致、字号可读、对齐、层级、bullet 缩进、日期对齐、无中文断字、无 ATS 敌意元素。不默认「导出成功=正确」。
5. 生成 Match Report：Target Role、Selected Base、Overall Match、Strong/Partial Matches、Missing Requirements、JD Keywords Used、JD Keywords NOT Used（因不支持）、Experiences Prioritized/De-emphasized、Changes from Base、Potential Interview Risks、Truthfulness/Evidence Warnings。
6. 版本命名：`YYYY-MM-<Company>-<Role>-vN`，不无谓覆盖旧版；写入 `archive/` 留历史。

## 输出
`Candidate_Role_Company.md/.docx/.pdf/_match_report.md` 四件套 + 版本位置。
