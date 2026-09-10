# FACT_RULES.md —— 真实性红线与证据状态

> 本规则是系统最高优先级规则。任何 Skill 在提取、改写、生成事实时都必须遵守。

## 1. 证据状态（Evidence Status）

每个重要事实必须有一个状态：

| 状态 | 定义 | 能否自动进入简历 |
|---|---|---|
| `VERIFIED` | 原始材料明确支持，可安全写入简历 | ✅ |
| `SAFE_INTERPRETATION` | 原始材料未逐字写出，但可合理总结、不改变事实含义 | ✅ |
| `UNVERIFIED` | 仅存在于用户记忆 / 历史简历，目前缺乏足够证据 | ❌ 需补证据 |
| `CONFLICT` | 不同 Source 对同一事实存在冲突 | ❌ 必须用户确认 |
| `DO_NOT_CLAIM` | 没有做过 / 不能证明 / 明确不应写入 | ❌ 永不写入 |

## 2. 真实性边界（数字能圆、措辞能夸、沾边就写、事实不能编）

**写简历前，必须先读完所有材料**（experience_bank + registry + 全部原始证据），否则无从判断哪些做过、哪些没做过——不要想当然认为你没做过某件事。

**允许：**
- 数字四舍五入 / 按量级表述：146231 →「15 万」、3.8% →「约 4%」
- 措辞强化：有真实贡献时「参与」→「负责 / 主导」；突出亮点、弱化次要
- **沾边就写**：学过、用过、项目里沾过的方法 / 技术都写（回归、线性回归、假设检验、因果推断、A/B 测试等）
- 合理夸大程度

**JD 关键词尽量全覆盖**，用「掌握 / 熟练 / 熟悉 / 会用」这类表述（ATS 命中，面试可自圆）。

**禁止（不无中生有）：**
- 编造没做过的经历、公司、角色、日期、项目身份
- 编造面试里完全解释不了、毫无根据的工具 / 技术

> 判断「有没有做过 / 沾不沾边」依据真实材料，不是猜测。核心事实不编，方法技能沾边就写。

## 3. 证据溯源（Provenance）

重要 Resume Fact 必须可回溯到 Source。Evidence Registry 每个 fact 至少记录：

```
fact_id / experience / fact / status / source_file / source_type
source_location / page / sheet / cell_range / notebook_section
supporting_text / confidence / resume_safe / notes
```

示例：

- 「Reduced weekly preparation time from 3 hours to 1 hour」→ 必须知道来自哪段实习、哪个 Source、是否明确记录、是否 resume-safe。
- 「100K+ records」→ 必须知道是什么 records、哪段经历、什么 context、source、confidence。

## 4. 冲突处理（CONFLICT）

发现 Conflict 时：**不得静默二选一**。必须生成 CONFLICT REPORT，说明：

- Source A 说了什么
- Source B 说了什么
- 为何冲突
- 当前正在使用哪个事实
- 需要用户确认什么

## 5. 原始文件永久保留

完成 extraction 后**绝不删除原始文件**。Raw 文件保留在 `source/raw/`，只增不改。

## 6. 缺失 ≠ 不存在

`source/inbox/` 中暂时没有某类材料，不代表该经历不存在。先标记 `UNVERIFIED` 或「缺证据」，等后续材料补充，而不是直接判定「没有」。
