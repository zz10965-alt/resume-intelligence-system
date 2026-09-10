# ROLE_CLASSIFICATION.md —— 岗位方向分类规则

> 一个 JD 只能有一个 **PRIMARY CLASSIFICATION**，但可以有 **SECONDARY / OVERLAP TAGS**。

分类必须综合：Official Title + 核心职责 + 预期产出 + 方法 + 业务目标。**不要只看关键词。**

## 目标方向

- **CORE**：DA、BA、DS（analytics-oriented）、AI Analytics
- **EXPLORATORY / SPECIALIZED**：Risk、UXR、Product analytics 等（独立分类，不污染核心统计）

## 分类规则

### DA（Data Analyst）

路径：Data → Data Processing → Metrics → Monitoring → Deep Dive → Root Cause/Driver → Visualization → Insights

典型：SQL、Python、Dashboard、KPI、Anomaly、Funnel、User behavior、Campaign analysis、Product analytics。

### BA（Business Analyst，数据驱动型业务/策略/运营分析）

路径：Business Problem → Market/User/Ops Analysis → Opportunity/Problem Diagnosis → Business Insight → Strategy → Planning → Resource Allocation → Decision Support

典型：Business analysis、Strategy、Operations、Market research、Growth、Commercial analysis、Consumer insights、Planning。

> 注：这里的 BA 指数据驱动业务/策略分析，**不是**传统 IT Business Analyst。

### DS（Data Scientist，analytics-oriented）

路径：Data → Statistics → Experimentation → Causal Inference → Modeling → ML → Prediction/Evaluation/Optimization

- 目标是 analytics-oriented DS，不是 algorithm-heavy ML research / LLM research / 硬核算法工程。
- Official Title 是重要 prior：若明确为 Data Scientist 且职责与 statistics/experimentation/modeling/data mining/quantitative analysis 兼容，默认优先归 DS。

### AI Analytics

路径：Business/Data Problem → AI/LLM/Agent → Analytics → Automated Insight → Decision Support

可能包含：Data Agent、Text-to-SQL、Agent Flow、LLM analytics、automated analysis/reporting、intelligent attribution、AI-assisted analytics、Dify、LangChain、Agent evaluation。

> **关键区分**：仅仅「会用 ChatGPT/Claude/Copilot」≠ AI Analytics。**AI Literacy ≠ AI Analytics Development。**

### Specialized（独立分类，不强行归入 DA/BA/DS）

Risk、UXR、PM、DE、Cybersecurity、Algorithm、Finance Quant 等，独立归类。不要为了填满 DA/BA/DS 而强行归类。
