# Consensus - 费用报销管理

## 明确需求描述

### 功能概述
实现完整的费用报销管理模块，包含申请提交、多级审批、财务审核和付款处理。

### API 端点设计

| 方法 | 路径 | 描述 |
|------|------|------|
| POST | /expenses | 创建报销申请 |
| GET | /expenses/{id} | 获取报销详情 |
| GET | /expenses | 列出报销申请（支持筛选） |
| POST | /expenses/{id}/approve | 审批通过 |
| POST | /expenses/{id}/reject | 审批拒绝 |
| POST | /expenses/{id}/verify | 财务审核 |
| POST | /expenses/{id}/pay | 财务付款 |

### 状态流转

```
pending → approved → verified → paid
    ↓         ↓          ↓
 rejected  rejected   rejected
```

### 数据模型

#### ExpenseRequest
- id: int
- employee_id: int
- items: list[ExpenseItem]
- total_amount: float（自动计算）
- expense_type: str (travel/office_supplies/meals/transportation/other)
- description: str
- status: str (pending/approved/rejected/verified/paid)
- required_level: str (supervisor/manager/director)
- approver: str | None
- verifier: str | None
- payer: str | None
- created_at: float
- history: list[dict]

#### ExpenseItem
- category: str
- amount: float
- description: str

## 技术约束
- 遵循现有代码风格
- 使用内存存储
- 集成 OpenTelemetry 指标

## 验收标准
1. 所有 API 端点正常工作
2. 状态流转正确
3. 金额校验和审批级别计算正确
4. 指标正常采集
5. 模拟器生成测试流量
