---
name: earnings-team
description: >
  四大师并行解读财报。启动多个Agent从不同视角解读同一份财报，综合研判。
tags: [investing, earnings, multi-agent]
---

# 四大师并行解读财报

启动多个 Agent 并行从四大师视角解读财报，最后编辑成可发布的文章。

如用户未提供公司名和财报期间，用 `clarify` 询问。

## 执行流程

### 第一步：获取财报原文

用 `web_search` 和 `web_extract` 获取财报原文和关键数据。

### 第二步：并行解读（delegate_task）

```
delegate_task(tasks=[
  {
    "goal": "从段永平视角解读 {公司名} {期间} 财报",
    "context": "财报数据：...\n\n关注：商业模式是否仍然健康？收入结构变化？护城河是否在变宽？",
    "toolsets": ["web"]
  },
  {
    "goal": "从巴菲特视角解读 {公司名} {期间} 财报",
    "context": "财报数据：...\n\n关注：盈利能力趋势、现金流质量、估值变化、安全边际。",
    "toolsets": ["web"]
  },
  {
    "goal": "从芒格/李录视角解读 {公司名} {期间} 财报",
    "context": "财报数据：...\n\n关注：风险信号、管理层表态、行业趋势、长期确定性。",
    "toolsets": ["web"]
  }
])
```

### 第三步：综合研判

汇总四个视角，输出：
1. 一句话总结
2. 超/低于预期的具体项目
3. 四维评分变化
4. 对投资论文的影响
5. 下一步关注点

## 保存报告

写入 `~/workspace/ai-berkshire/reports/{公司名}/{公司名}-earnings-{期间}.md`
