# Acceptance - 费用报销管理

## 验收检查清单

### 功能验收
- [x] POST /expenses 创建报销申请
- [x] GET /expenses/{id} 获取报销详情
- [x] GET /expenses 列表查询（支持 status、employee_id 筛选）
- [x] POST /expenses/{id}/approve 审批通过
- [x] POST /expenses/{id}/reject 审批拒绝
- [x] POST /expenses/{id}/verify 财务审核
- [x] POST /expenses/{id}/pay 财务付款

### 业务逻辑验收
- [x] 金额自动计算（多个费用项求和）
- [x] 审批级别自动计算（≤500 supervisor, ≤2000 manager, >2000 director）
- [x] 状态流转正确（pending → approved → verified → paid / rejected）
- [x] 历史记录追踪（每次操作记录到 history）

### 技术验收
- [x] OpenTelemetry 指标集成（4个 Counter）
- [x] 模拟器集成（5个报销相关 action）
- [x] 测试用例通过（6个测试用例）
- [x] 无 linter 错误
- [x] README 文档更新

## 测试结果

```
tests/test_app.py::test_expense_request_flow PASSED
tests/test_app.py::test_expense_rejection_flow PASSED
tests/test_app.py::test_expense_approval_level_calculation PASSED
tests/test_app.py::test_expense_list_filter PASSED
tests/test_app.py::test_expense_invalid_type PASSED
tests/test_app.py::test_expense_empty_items PASSED

======================== 6 passed ========================
```

## 验收结论

✅ **所有验收标准已满足**
