# MARKET_RULES.md —— 市场分析与 JD 处理规则

## 1. 中美分离

中国与美国市场**必须分开**分析、分开存储、分开建简历变体。

市场画像：

- China：`CN_DA` `CN_BA` `CN_DS` `CN_AI_Analytics`
- US：`US_DA` `US_BA` `US_DS`
- Risk / UXR 等可独立研究，但**不污染** DA/BA/DS 核心统计。

## 2. 市场画像输出结构

每个 Market Profile 输出：Role Definition、高频技术技能、高频分析方法、高频业务技能、高频工具、高频职责、高频交付物、Preferred/Bonus 技能、常见教育要求、Entry-level 期望、行业模式、低频要求、值得包含的关键词、不值得过度拟合的关键词、Candidate Coverage、Candidate Gaps（HIGH/MEDIUM/LOW PRIORITY / DO NOT FAKE）。

## 3. JD 清洗（Excel 特别注意）

- Excel 的 max row / used range ≠ 真实 JD 数量。某些 Sheet 因格式化/删除单元格/复制格式/历史编辑，显示几百上千行，**必须按实际有内容的 JD 计算**。
- 步骤：remove empty rows → normalize fields → detect duplicates → detect near-duplicate → preserve source sheet / company / title / JD text / market / Core-Reference 状态。

## 4. JD 加权

优先级：Core New Grad / Campus > Early Career relevant > Reference > Internship reference。

- 同一公司高度相似的两个 JD **不算两个独立市场信号**。
- **Company Diversity > Duplicate Volume**。不要因某家企业发布大量相似岗位而让它支配整个 Market Profile。

## 5. 去重原则

同一个 JD 出现在两个 Sheet，不应自动算两份市场信号。先按「内容 + 公司 + 标题」去重。

## 6. JD 库 Sheet 处理

`JD search.xlsx` 有多个 Sheet（可能含：岗位方向KW、DA JD国内、BA JD国内、DS JD国内、AI的分析JD、风控分析JD、用户研究JD、DA JD US、BA JD US、DS JD US、实习可考虑投递 等）。

- **必须读所有相关 Sheet，不要只分析一个。**
- **不要假设 Sheet 名永远不变，先 inspect workbook structure。**
