---
name: 研报数据源
description: 研报数据源，东财+akshare
type: reference
---

# 研报数据源

## akshare

- **版本**: 1.18.58
- **安装**: `pip install akshare`
- **状态**: 已安装可用

### 东财研报接口
```python
import akshare as ak
# 个股研报
df = ak.stock_research_report_em(symbol='000001')
# 返回224条记录，包含评级、盈利预测、PDF链接等

# 个股公告研报
df = ak.stock_individual_notice_report(security='000001', symbol='公告', begin_date='20260101', end_date='20260511')
```

### 研报相关函数
- `stock_research_report_em` - 东财个股研报
- `stock_individual_notice_report` - 东财个股公告
- `fund_announcement_report_em` - 基金公告
- `stock_financial_report_sina` - 新浪财报

### 返回字段
- 股票代码、股票名称
- 评级、目标价
- 盈利预测（2026-2028）
- 行业、机构
- PDF链接