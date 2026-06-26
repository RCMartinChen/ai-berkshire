# AI Berkshire — Hermes Agent 适配版

## 项目概述

基于 [Hermes Agent](https://hermes-agent.nousresearch.com) 的价值投资研究 Skill 合集。
四大师框架：巴菲特、芒格、段永平、李录。

**上游仓库**: https://github.com/xbtlin/ai-berkshire
**Fork 仓库**: https://github.com/RCMartinChen/ai-berkshire

## 项目结构

```
skills/          — 原始投研 Skill 定义（Claude Code 格式）
tools/           — 辅助工具（financial_rigor.py 精确计算等）
reports/         — 投资研究报告输出
筛选公司/        — 筛选结果存档
实盘记录/        — 实盘操作记录
```

## Hermes 适配

Hermes Agent 的 skills 安装在 `~/.hermes/skills/value-investing/` 下，共 19 个：

| Skill | 用途 |
|-------|------|
| `ai-berkshire` | 框架概览与工具指南 |
| `investment-team` | 四大师并行投研（delegate_task 并行） |
| `investment-research` | 四大师综合深度分析（顺序执行） |
| `investment-checklist` | 巴菲特买入前6关快速筛选 |
| `quality-screen` | 7条去劣指标快速排除 |
| `news-pulse` | 股价异动10分钟归因 |
| `earnings-review` | 财报精读 |
| `earnings-team` | 四大师并行解读财报 |
| `thesis-tracker` | 投资论文跟踪 |
| `portfolio-review` | 组合管理与优化 |
| `management-deep-dive` | 管理层纵深研究 |
| `industry-research` | 行业全景研究 |
| `industry-funnel` | 行业漏斗筛选 |
| `private-company-research` | 未上市公司研究 |
| `deep-company-series` | 8篇长文系列拆解 |
| `dyp-ask` | 段永平思维方式 |
| `bottleneck-hunter` | 瓶颈猎手扫描 |
| `financial-data` | 数据收集规范 |
| `wechat-article` | 公众号文章生成 |

## Claude Code → Hermes 适配映射

| Claude Code | Hermes |
|-------------|--------|
| `$ARGUMENTS` | 从用户消息提取参数 |
| `TeamCreate` + `TaskCreate` | `delegate_task` (tasks 数组并行) |
| `SendMessage` (agent 间通信) | subagent 返回 summary |
| `WebSearch` / `WebFetch` | `web_search` / `web_extract` |
| `~/.claude/commands/xxx.md` | `~/.hermes/skills/value-investing/xxx/SKILL.md` |
| `~/ai-berkshire/tools/` | `~/workspace/ai-berkshire/tools/` |

## 工具

所有工具位于 `tools/` 目录，零外部依赖，Python ≥ 3.7：

- `financial_rigor.py` — 精确金融计算（decimal.Decimal，28位精度）
- `stock_screener.py` — 动量发现+价值验证选股
- `ashare_data.py` — A股数据（零依赖）
- `morningstar_fair_value.py` — 晨星公允价值
- `xueqiu_scraper.py` — 雪球爬虫
- `report_audit.py` — 报告数据抽检

## 同步上游

```bash
cd ~/workspace/ai-berkshire
git pull --rebase upstream main
```

## 报告目录结构

所有报告按**公司名**建文件夹，详见原始 CLAUDE.md。
