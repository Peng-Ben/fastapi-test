# Task - 费用报销管理

## 任务依赖图

```mermaid
flowchart LR
    T1[1.定义Pydantic模型] --> T2[2.添加指标定义]
    T2 --> T3[3.初始化存储]
    T3 --> T4[4.实现创建接口]
    T4 --> T5[5.实现查询接口]
    T5 --> T6[6.实现审批接口]
    T6 --> T7[7.实现财务接口]
    T7 --> T8[8.更新模拟器]
    T8 --> T9[9.更新文档]
    T9 --> T10[10.测试验证]
```

## 子任务清单

### T1: 定义 Pydantic 模型
- **输入**: DESIGN 文档中的模型定义
- **输出**: 在 main.py 中添加模型类
- **验收**: 模型类定义完整，类型注解正确

### T2: 添加指标定义
- **输入**: DESIGN 文档中的指标定义
- **输出**: 在 main.py 中添加 Counter 指标
- **验收**: 4 个指标定义完成

### T3: 初始化存储
- **输入**: 现有 app.state 模式
- **输出**: app.state.expenses, app.state.next_expense_id
- **验收**: 存储结构初始化

### T4: 实现创建接口
- **输入**: POST /expenses 规范
- **输出**: create_expense 函数
- **验收**: 可创建报销申请，金额计算正确，审批级别正确

### T5: 实现查询接口
- **输入**: GET /expenses/{id}, GET /expenses 规范
- **输出**: get_expense, list_expenses 函数
- **验收**: 可查询单个和列表

### T6: 实现审批接口
- **输入**: POST /expenses/{id}/approve, /reject 规范
- **输出**: approve_expense, reject_expense 函数
- **验收**: 状态流转正确，历史记录正确

### T7: 实现财务接口
- **输入**: POST /expenses/{id}/verify, /pay 规范
- **输出**: verify_expense, pay_expense 函数
- **验收**: 状态流转正确，历史记录正确

### T8: 更新模拟器
- **输入**: 现有 Simulator 模式
- **输出**: sim.py 中添加报销相关 action
- **验收**: 模拟器可生成报销流量

### T9: 更新文档
- **输入**: 新增 API
- **输出**: README.md 更新
- **验收**: 文档完整

### T10: 测试验证
- **输入**: 所有接口
- **输出**: 测试用例
- **验收**: 测试通过
