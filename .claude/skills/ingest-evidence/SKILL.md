---
name: ingest-evidence
description: Ingest new raw evidence files (PDF/DOCX/PPTX/XLSX/CSV/IPYNB/PY/SQL/MD/TXT/images) placed in source/inbox, extract facts, classify evidence status, update Evidence Registry and Experience Bank, and report conflicts. Use when the user provides new source material, says "ingest this", "ingest <file>", or drops files into source/inbox.
---

# Ingest Evidence

把 `source/inbox/` 里的新原始文件摄入系统：提取事实 → 分级 → 更新 Registry + Experience Bank → 报告冲突。**绝不删除原始文件。**

## 前置规则（必读）
- `rules/FACT_RULES.md`（证据状态、真实性红线、冲突处理）
- `source/evidence_registry/README.md`（registry 字段）
- `source/experience_bank/README.md`（经历库结构）

## 步骤

1. **识别文件**：列出 `source/inbox/` 下待处理文件，识别类型。
2. **读取文件**：按类型读取（PDF 用页码、XLSX 读所有 sheet、IPYNB 读 cell、PY/SQL/MD/TXT 直接读、图片用视觉读取）。缺失的解析工具先确认可用性。
3. **归属判断**：判断属于哪段 Internship / Project / Education / Skill。
4. **提取**：business/project context、dataset、data scale、methods、technologies、metrics、quantitative findings、business findings、responsibilities、deliverables、impact、recommendations。
5. **与现有经历库比较**：查重/查冲突/补缺。
6. **分级**：对每个事实标 `VERIFIED` / `SAFE_INTERPRETATION` / `UNVERIFIED` / `CONFLICT`（定义见 FACT_RULES.md）。
7. **更新 Evidence Registry**：`source/evidence_registry/registry.yaml` 增量追加，fact_id 自增。
8. **更新 Experience Bank**：写入/更新对应 `source/experience_bank/` 条目；resume-safe bullets 带 status + fact_id。
9. **冲突处理**：发现 `CONFLICT` → 生成 CONFLICT REPORT（Source A vs B、为何冲突、当前用哪个、需用户确认什么），**不静默二选一**。
10. **归档 Raw**：把文件从 `inbox/` 移到 `source/raw/` 对应子目录（internships/projects/education/resumes/misc），**不删除**。

## 输出
- 已摄入文件清单 + 每个文件的 fact 数量与状态分布
- 新增/更新的 experience 条目
- CONFLICT REPORT（若有）
- 待用户确认的事项（若有）
