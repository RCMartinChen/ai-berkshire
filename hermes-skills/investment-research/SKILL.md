---
name: investment-research
description: >
  四大师综合深度投资研究框架。按7个模块顺序执行：生意本质（段永平）→护城河（巴菲特）→逆向思考（芒格）→管理层→行业趋势（李录）→估值→综合决策。
tags: [investing, value-investing, research]
---

# 投资研究：四大师综合分析框架

对用户指定的公司进行基于巴菲特-芒格-段永平-李录四大师方法论的系统化深度研究。

如用户未提供公司名，用 `clarify` 询问。

## 核心流程

研究按以下顺序执行，包含一个**强制性前置步骤**和七个主要模块：

### 前置步骤：AI研究偏见自觉

评估公司的 **"信息丰富度评级"**（A/B/C），识别AI分析陷阱：

| 等级 | 特征 | AI研究陷阱 | 应对策略 |
|------|------|-----------|---------|
| A级 | 上市多年、覆盖多 | 共识过强，AI输出趋同市场 | **做反面检验**：聪明人为什么不买？ |
| B级 | 上市1-3年、覆盖有限 | AI用"合理推测"填补空白 | **标注置信度** |
| C级 | 刚上市/冷门股 | AI因资料不足而过度保守 | **用第一性原理提问** |

**偏见自查清单**（研究全程使用）：
- 我的"确定性"感受是来自生意本质，还是来自资料数量？
- 如果把资料量减少一半，我的结论会变吗？
- AI输出的分析是否与市场共识高度雷同？

### 第一步：数据收集与交叉验证

使用 `web_search` 搜索数据。数据源规范：
- 美股：macrotrends + stockanalysis
- 港股：aastocks + macrotrends ADR
- A股：东方财富 + 巨潮资讯

**必须通过工具验证**：
```bash
python3 ~/workspace/ai-berkshire/tools/financial_rigor.py verify-market-cap \
  --price {股价} --shares {总股本} --reported {报告市值} --currency {币种}

python3 ~/workspace/ai-berkshire/tools/financial_rigor.py cross-validate \
  --field {字段名} --values '{\"来源1\": 数值, \"来源2\": 数值}' --unit {单位}

python3 ~/workspace/ai-berkshire/tools/financial_rigor.py verify-valuation \
  --price {股价} --eps {EPS} --bvps {每股净资产}
```

### 第二步：生意本质分析（段永平"对的生意"）

核心分析：定义生意本质、收入结构拆解、5年盈利能力趋势、商业模式画布、生态粘性。

**必须执行收入漏斗分析**：绘制从业务量到自由现金流的完整漏斗，逐层标注金额、比率和具体去向。

**关键追问**："这门生意好在哪？如果只能用一句话描述，是什么？"

### 第三步：护城河评估（巴菲特"经济护城河"）

逐一验证五类护城河：品牌/定价权、转换成本、网络效应、规模效应、技术/专利壁垒。

**关键追问**："10年后这条护城河还在吗？什么能摧毁它？"

### 第四步：逆向思考与风险清单（芒格"反过来想"）

列出公司失败的所有路径（概率、影响程度）。进行历史类比、跨学科分析。收集空方核心论点。

**关键追问**："我最可能在哪里犯错？聪明人为什么会不买/做空这家公司？"

### 第五步：管理层评估（段永平"对的人" & 巴菲特"诚信"）

复盘CEO/创始人关键决策。评估资本配置能力、股东利益一致性。

**关键追问**："如果CEO退休，这家公司还能保持竞争力吗？"

### 第六步：行业与文明趋势（李录"文明演进框架"）

判断行业是否处于"文明级范式转移"。分析TAM增长曲线、公司在价值链中的位置。

**关键追问**："站在20年后回看，这家公司是'标准石油'还是'3Com'？"

### 第七步：估值与安全边际（巴菲特 & 段永平）

**必须通过工具验算**：
```bash
python3 ~/workspace/ai-berkshire/tools/financial_rigor.py three-scenario \
  --price {股价} --eps {EPS} --shares {总股本亿} \
  --growth {乐观增速} {中性增速} {悲观增速} \
  --pe {乐观PE} {中性PE} {悲观PE} --years 3 --currency {币种}
```

**关键追问**："如果股市明天关闭5年，你愿意以这个价格持有吗？"

### 第八步：综合决策备忘录

汇总各维度结论及信心度。给出对空仓者、持仓者的明确策略建议（买入/观望/回避）。

## 输出要求

1. 报告以"信息丰富度评级"和"AI研究局限性声明"开头
2. 所有分析必须有数据支撑（附来源）
3. 使用Markdown表格呈现关键数据
4. 每个模块末尾有对应大师的"追问"
5. 估值必须给出具体价格区间
6. 结尾区分"AI分析置信度"与"投资确定性"

## 保存报告

写入 `~/workspace/ai-berkshire/reports/{公司名}/{公司名}-research-{YYYYMMDD}.md`

## 数据抽检（准出流程）

```bash
python3 ~/workspace/ai-berkshire/tools/report_audit.py extract --report <报告文件路径>
python3 ~/workspace/ai-berkshire/tools/report_audit.py verdict --results '<JSON>' --report <报告文件名>
```
