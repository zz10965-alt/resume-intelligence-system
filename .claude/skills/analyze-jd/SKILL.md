---
name: analyze-jd
description: Analyze a single job description (JD): classify role family (DA/BA/DS/AI Analytics/Specialized), identify market (China/US), extract responsibilities/skills/keywords, assess candidate match against the Experience Bank, and recommend a base resume. Use when the user provides one JD and asks to analyze it or "generate a resume for this JD".
---

# Analyze JD

解析单个 JD：分类 + 市场 + 关键词 + 与经历库匹配 + 推荐 Base。

## 前置规则
- `rules/ROLE_CLASSIFICATION.md`（分类规则，不看关键词、综合判断）
- `rules/MARKET_RULES.md`（中美区分、去重）
- `source/experience_bank/`（候选真实能力）

## 步骤

1. **解析 JD**：market（China/US）、role family、seniority、industry、business context、responsibilities、required skills、preferred skills、ATS keywords。
2. **分类**：给一个 PRIMARY 分类（DA/BA/DS/AI Analytics/Specialized），可加 SECONDARY/OVERLAP tags。区分 AI Literacy vs AI Analytics Development。
3. **提取关键词**：技能、方法、工具、交付物。
4. **匹配经历库**：JD 要求 vs Experience Bank 现有能力 → Strong / Partial / Missing。
5. **推荐 Base**：给出应使用的 Base Resume Variant（如 CN_DA、US_DS）。
6. **输出差距**：区分「真实具备但未写」「真实具备但证据不足（UNVERIFIED）」「缺失（GAP，不能编造）」。

## 输出
分类结论、市场、关键词清单、候选匹配表、推荐 Base、差距清单。
