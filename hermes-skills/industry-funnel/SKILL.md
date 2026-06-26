---
name: industry-funnel
description: >
  行业漏斗筛选。全市场→粗筛≤10家→终选3家深度分析。
tags: [investing, screening, industry]
---

# 行业漏斗筛选

全市场 → 粗筛≤10家 → 终选3家深度分析的漏斗筛选。

如用户未提供行业/主题，用 `clarify` 询问。

## 漏斗流程

### 第一层：全市场扫描
- 用 `web_search` 搜索该行业所有上市公司
- 列出完整清单（可能20-50家）

### 第二层：快速粗筛（去劣7指标）
- 使用 `quality-screen` skill 的7条去劣指标
- 排除不达标公司
- 剩余 ≤10 家

### 第三层：深度对比
- 对粗筛通过的公司进行详细对比
- 商业模式、财务数据、估值、护城河
- 终选 3 家

### 第四层：终选3家深度分析
- 对3家公司各出一份简要投研报告
- 给出排序和投资建议

## 保存报告

写入 `~/workspace/ai-berkshire/reports/{行业名}-funnel-{YYYYMMDD}.md`
