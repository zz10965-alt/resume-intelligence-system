---
name: analyze-market
description: Build or update a market profile (e.g. CN_DA, US_DS) from the JD database: aggregate high-frequency skills/methods/tools/responsibilities, deduplicate and weight JDs, and produce candidate coverage/gaps. Use when the user asks to analyze a market, update market profiles, or after adding new JDs.
---

# Analyze Market

基于 JD 库生成/更新某个市场画像（如 `CN_DA`、`US_DS`）。

## 前置规则
- `rules/MARKET_RULES.md`（中美分离、JD 加权、去重、Excel 真实 JD 数量）
- `rules/ROLE_CLASSIFICATION.md`（先正确分类）

## 步骤

1. **确定范围**：目标市场（China/US）+ 方向（DA/BA/DS/AI Analytics）。
2. **取 JD**：从 `jd/processed/` 取已清洗、已分类的该市场 JD。
3. **清洗与去重**：remove empty rows、normalize fields、detect duplicates / near-duplicates；同公司相似 JD 不算独立信号，Company Diversity > Duplicate Volume。
4. **加权**：Core New Grad/Campus > Early Career > Reference > Internship reference。
5. **聚合统计**：高频技能/方法/工具/职责/交付物、Preferred/Bonus、教育要求、行业模式、低频要求。
6. **候选覆盖与差距**：对照 `source/experience_bank/` 输出 Coverage / Gaps（HIGH/MEDIUM/LOW PRIORITY / DO NOT FAKE）。
7. **写画像**：写入 `market_profiles/<china|us>/<XX_YY>.md`（覆盖旧版，保留 changelog）。

## 输出
更新后的 Market Profile 文件 + 关键发现摘要 + 与上一版的差异。
