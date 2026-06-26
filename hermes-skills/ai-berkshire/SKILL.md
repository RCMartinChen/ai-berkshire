---
name: ai-berkshire
description: >
  AI Berkshire 价值投资研究框架概览与工具指南。基于巴菲特·芒格·段永平·李录四大师方法论。
  Fork 自 xbtlin/ai-berkshire，适配 Hermes Agent。
tags: [investing, value-investing, finance, research]
---

# AI Berkshire — 价值投资研究框架

## 项目位置

- **本地仓库**: `~/workspace/ai-berkshire/`
- **上游仓库**: https://github.com/xbtlin/ai-berkshire
- **Fork 仓库**: https://github.com/RCMartinChen/ai-berkshire

## 四大师框架

| 大师 | 视角 | 核心追问 |
|------|------|----------|
| 段永平 | 生意本质 | "这门生意好在哪？一句话描述是什么？" |
| 巴菲特 | 护城河+安全边际 | "10年后这条护城河还在吗？" |
| 芒格 | 逆向思考+风险排查 | "我最可能在哪里犯错？聪明人为啥不买？" |
| 李录 | 文明趋势+范式转移 | "20年后回看，是标准石油还是3Com？" |

## 工具清单

所有工具位于 `~/workspace/ai-berkshire/tools/`，零外部依赖，Python ≥ 3.7。

### financial_rigor.py — 精确金融计算

```bash
# 市值验算
python3 ~/workspace/ai-berkshire/tools/financial_rigor.py verify-market-cap \
  --price {股价} --shares {总股本} --reported {报告市值} --currency {币种}

# 估值验算（PE/PB/ROE/FCF Yield等）
python3 ~/workspace/ai-berkshire/tools/financial_rigor.py verify-valuation \
  --price {股价} --eps {EPS} --bvps {每股净资产} --fcf-per-share {每股FCF} --dividend {每股股息}

# 多源数据交叉验证
python3 ~/workspace/ai-berkshire/tools/financial_rigor.py cross-validate \
  --field {字段名} --values '{"来源1": 数值, "来源2": 数值}' --unit {单位}

# 三情景估值（乐观/中性/悲观）
python3 ~/workspace/ai-berkshire/tools/financial_rigor.py three-scenario \
  --price {股价} --eps {EPS} --shares {股本亿} \
  --growth {乐观增速} {中性增速} {悲观增速} \
  --pe {乐观PE} {中性PE} {悲观PE} --years 3 --currency {币种}

# Benford定律检测财务造假
python3 ~/workspace/ai-berkshire/tools/financial_rigor.py benford \
  --values '[1234, 2345, 3456, ...]'

# 精确计算器
python3 ~/workspace/ai-berkshire/tools/financial_rigor.py calc --expr '510 * 9.11e9'
```

### stock_screener.py — 动量发现+价值验证选股

```bash
# 扫描全部 watchlist
python3 ~/workspace/ai-berkshire/tools/stock_screener.py

# 扫描指定股票
python3 ~/workspace/ai-berkshire/tools/stock_screener.py NVDA TSLA GOOG

# 更新基本面数据
python3 ~/workspace/ai-berkshire/tools/stock_screener.py --update MU
```

### 其他工具

| 工具 | 命令 | 用途 |
|------|------|------|
| `ashare_data.py` | `python3 tools/ashare_data.py` | A股数据（零依赖） |
| `morningstar_fair_value.py` | `python3 tools/morningstar_fair_value.py` | 晨星公允价值（840股） |
| `xueqiu_scraper.py` | `python3 tools/xueqiu_scraper.py --user-id {ID}` | 雪球爬虫 |
| `report_audit.py` | `python3 tools/report_audit.py extract/verdict` | 报告数据抽检 |

## 可用 Skills

在 Hermes 中使用以下命令触发对应分析：

| Skill 名称 | 用途 | 触发方式 |
|------------|------|----------|
| `investment-checklist` | 巴菲特买入前6关快速筛选 | "用 investment-checklist 分析腾讯" |
| `investment-research` | 四大师综合深度分析 | "用 investment-research 分析腾讯" |
| `investment-team` | 4 Agent 并行投研团队 | "用 investment-team 分析腾讯" |
| `quality-screen` | 7条指标快速排除非一流公司 | "用 quality-screen 筛选港股互联网" |
| `news-pulse` | 股价异动10分钟归因 | "用 news-pulse 分析腾讯下跌原因" |
| `earnings-review` | 财报精读 | "用 earnings-review 分析腾讯Q4财报" |
| `earnings-team` | 四大师并行解读财报 | "用 earnings-team 分析腾讯财报" |
| `thesis-tracker` | 投资论文跟踪 | "用 thesis-tracker 跟踪腾讯" |
| `portfolio-review` | 组合管理与优化 | "用 portfolio-review 审视持仓" |
| `management-deep-dive` | 管理层纵深研究 | "用 management-deep-dive 分析腾讯管理层" |
| `industry-research` | 行业全景研究 | "用 industry-research 研究AI算力行业" |
| `industry-funnel` | 全市场漏斗筛选 | "用 industry-funnel 筛选新能源" |
| `private-company-research` | 未上市公司研究 | "用 private-company-research 研究蚂蚁集团" |
| `deep-company-series` | 8篇长文系列拆解 | "用 deep-company-series 拆解腾讯" |
| `dyp-ask` | 段永平思维方式思考 | "用 dyp-ask 思考XXX问题" |
| `bottleneck-hunter` | 瓶颈猎手扫描 | "用 bottleneck-hunter 扫描腾讯" |

## 报告目录结构

所有报告保存在 `~/workspace/ai-berkshire/reports/`，按公司名建文件夹。

## 数据源规范

| 市场 | 主源 | 副源 |
|------|------|------|
| 美股 | macrotrends | stockanalysis |
| 港股 | aastocks | macrotrends ADR |
| A股 | 东方财富 | 巨潮资讯 |

**关键数据必须来自两个独立来源，误差 >1% 须标记。**

## 同步上游

```bash
cd ~/workspace/ai-berkshire
git pull --rebase upstream main
```
