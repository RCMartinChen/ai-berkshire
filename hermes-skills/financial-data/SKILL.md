---
name: financial-data
description: >
  财务数据获取与交叉验证规范。定义数据源、验证流程、工具调用标准。
tags: [investing, data, validation]
---

# 财务数据获取与交叉验证规范

本 skill 定义了投研分析中财务数据的获取标准和验证流程。

## 数据源规范

| 市场 | 主源 | 副源 | 备注 |
|------|------|------|------|
| 美股 | macrotrends.net | stockanalysis.com | 两源误差>1%须标记 |
| 港股 | aastocks.com | macrotrends（ADR） | 港股数据需注意币种 |
| A股 | 东方财富 | 巨潮资讯 | 注意人民币单位 |

## 必须验证的数据点

1. 总股本
2. 当前股价和市值
3. 最近财年收入和净利润
4. 现金储备和净现金
5. 管理层持股比例

## 工具调用

```bash
# 市值验算
python3 ~/workspace/ai-berkshire/tools/financial_rigor.py verify-market-cap \
  --price {股价} --shares {总股本} --reported {报告市值} --currency {币种}

# 估值验算
python3 ~/workspace/ai-berkshire/tools/financial_rigor.py verify-valuation \
  --price {股价} --eps {EPS} --bvps {每股净资产}

# 交叉验证
python3 ~/workspace/ai-berkshire/tools/financial_rigor.py cross-validate \
  --field {字段} --values '{\"源1\": 值, \"源2\": 值}' --unit {单位}
```

## 验证规则

- 优先采用公司年报/交易所数据
- 工具输出嵌入报告附录
- 工具报告偏差过大必须排查
- **禁止LLM心算**，必须通过工具程序化验证
