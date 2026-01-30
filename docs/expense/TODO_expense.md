# TODO - 费用报销管理

## 已完成
- [x] 基础 CRUD 功能
- [x] 审批流程
- [x] 财务处理流程
- [x] 指标集成
- [x] 模拟器集成
- [x] 测试用例

## 待办事项（可选扩展）

### 功能扩展
- [ ] 附件/发票上传支持
- [ ] 报销额度限制
- [ ] 报销统计看板（按部门、类型统计）
- [ ] 报销导出功能

### 流程优化
- [ ] 多级审批链（超过一定金额需要多人审批）
- [ ] 自动提醒（审批超时提醒）
- [ ] 驳回后重新提交

## 使用说明

### 创建报销申请
```bash
curl -X POST http://localhost:8000/expenses \
  -H "Content-Type: application/json" \
  -d '{
    "employee_id": 1000,
    "expense_type": "travel",
    "items": [
      {"category": "transport", "amount": 150.00, "description": "taxi"},
      {"category": "meals", "amount": 80.00, "description": "lunch"}
    ],
    "description": "business trip"
  }'
```

### 审批通过
```bash
curl -X POST http://localhost:8000/expenses/1/approve \
  -H "Content-Type: application/json" \
  -d '{"approver": "supervisor_1"}'
```

### 财务审核
```bash
curl -X POST http://localhost:8000/expenses/1/verify \
  -H "Content-Type: application/json" \
  -d '{"verifier": "finance_1"}'
```

### 付款
```bash
curl -X POST http://localhost:8000/expenses/1/pay \
  -H "Content-Type: application/json" \
  -d '{"payer": "finance_2", "payment_ref": "PAY-12345"}'
```
