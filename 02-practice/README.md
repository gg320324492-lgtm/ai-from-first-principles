# 02-practice — 动手实现区

> 所有"要跑起来的代码"都在这里：从零实现的项目 + 评估基准套件。
> 每个项目独立可运行，自带 README、测试与复现说明。

## 目录说明

| 目录 | 内容 | 对应阶段 |
|------|------|----------|
| `01-micrograd/` | 手写自动微分引擎：Value 类、MLP、优化器 | 阶段Ⅰ（Week 1–3） |
| `02-tinygpt/` | 从零实现 GPT：分词器、Attention、训练与生成 | 阶段Ⅱ（Week 4–7） |
| `03-finetuning/` | 微调与对齐：SFT 数据构造、LoRA、DPO 对照 | 阶段Ⅲ（Week 8–11） |
| `04-mini-agent/` | Agent 内核：Agent Loop、工具调用、状态管理 | 阶段Ⅴ（Week 15–17） |
| `05-research-agent/` | 高级 Agent：RAG、Memory、Planning、多 Agent | 阶段Ⅵ（Week 18–21） |
| `06-benchmark-suite/` | 评估套件：任务集、自动评分器、消融脚本 | 阶段Ⅶ（Week 22–24） |

## 项目内结构约定

```
0X-项目名/
├── README.md          # 运行方式、依赖、复现命令
├── src/ 或平铺 .py    # 实现代码
├── test_*.py          # 单元测试（数值验证）
└── notebooks/         # 可选：演示用 notebook
```

## 代码规则（详见 LEARNING_RULES.md）

- **学习保护**：本周正在学的核心模块自己写，Agent 只给提示；脚手架/测试/可视化可由 Agent 代写。
- 每个核心实现必须有数值验证测试（有限差分、恒等式、解析解对照）。
- 优先标准库 + numpy；先从零实现，再学成熟框架。
- 阶段结束打 tag：`stage-1-micrograd`、`stage-2-tinygpt` …

## 与其他区的关系

- 实现过程中的理解 → 记到 `01-learning/notes/` 或 `derivations/`
- 写错的地方 → 记到 `01-learning/mistakes/`
- 跑出的结果 → 存到 `03-experiments/`，此处只放代码
- 大文件（权重/数据集）不入库，见 `.gitignore`
