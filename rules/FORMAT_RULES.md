# FORMAT_RULES.md —— 简历排版规范

## 1. 整体

专业、干净、现代但保守、ATS 友好、recruiter 友好、6–10 秒可扫读、应届生优先一页。

## 2. 结构（默认顺序）

```
NAME / CONTACT
EDUCATION
PROFESSIONAL EXPERIENCE
PROJECT EXPERIENCE
TECHNICAL SKILLS
```

- 顺序可因市场/角色有正当理由而调整。
- Experience 一般应在 Projects 之前。

## 3. 避免

照片、skill bar、装饰图表、复杂多栏、过多图标、破坏 ATS 的图形、多余颜色、导致解析问题的文本框。

## 4. 一页排版校验（PDF 导出后视觉校验）

- 恰好（或最好）一页
- 无文字溢出、无裁切
- 边距一致、间距一致、字体一致
- 字号可读
- 对齐、层级、bullet 缩进、日期对齐
- 无中文断字
- 无 ATS 敌意元素

> 不要默认「导出成功 = 排版正确」，必须实际视觉校验。

## 5. 文件格式架构

```
Markdown（机器可编辑的规范源，Git 版本控制 + diff）
   ↓
DOCX（人工可编辑交付物）
   ↓
PDF（最终投递交付物）
```

每个最终简历产出：`Candidate_Role_Company.md` / `.docx` / `.pdf` / `_match_report.md`

> 若 Typst / HTML / CSS / Pandoc / LaTeX 能提供更可靠的一页输出，可提出，但必须满足：可编辑源 + DOCX + PDF + ATS 友好 + 中英兼容 + 布局稳定 + 可复现 + 易维护。
