# ROADMAP — 24 周学习路线

> 每周建议投入 8–10 小时。节奏可根据掌握情况调整，但不跳过核心原理。
> 每周结束在 `01-learning/weekly/week-XX.md` 归档记录。

## 总览

| 阶段 | 周数 | 核心内容 | 阶段交付物 |
|------|------|----------|------------|
| Ⅰ. 神经网络基础 | 1–3 | 梯度、自动微分、反向传播、优化器 | 手写 Micrograd |
| Ⅱ. Transformer | 4–7 | Tokenizer、Attention、GPT 架构 | TinyGPT |
| Ⅲ. 训练与对齐 | 8–11 | 预训练、SFT、LoRA、DPO、RLHF | 微调实验报告 |
| Ⅳ. 模型推理 | 12–14 | KV Cache、量化、采样、推理加速 | 推理性能基准 |
| Ⅴ. Agent 内核 | 15–17 | Agent Loop、工具调用、状态管理、MCP | MiniAgent |
| Ⅵ. 高级 Agent | 18–21 | RAG、Memory、Planning、多 Agent | ResearchAgent |
| Ⅶ. 评估与优化 | 22–24 | Benchmark、Tracing、可靠性、消融 | 完整技术报告 |

---

## 阶段Ⅰ：神经网络基础（第 1–3 周）

**目标**：从标量自动微分开始，彻底理解反向传播与训练循环。

### Week 1 — 计算图与梯度
- [ ] 导数、链式法则、多元函数梯度
- [ ] 计算图：前向传播即图的求值
- [ ] 手工推导：线性回归 + MSE 的梯度
- [ ] 实现：`Value` 类（标量自动微分，支持 +、*、tanh）
- 实验：与数值梯度（有限差分）对比验证

### Week 2 — 反向传播与 MLP
- [ ] 反向传播 = 计算图上的逆拓扑序遍历
- [ ] MLP、激活函数、权重初始化
- [ ] 推导：两层网络的完整反向传播
- [ ] 实现：`Neuron` / `Layer` / `MLP`
- 实验：二分类玩具数据集，观察决策边界

### Week 3 — 优化与训练动力学
- [ ] SGD、Momentum、Adam 推导与直觉
- [ ] 学习率、batch size、初始化的影响
- [ ] 实现：三种优化器 + 训练循环
- [ ] **阶段交付物**：`02-practice/01-micrograd/`
- 实验：不同学习率/优化器的损失曲线对照

---

## 阶段Ⅱ：Transformer（第 4–7 周）

**目标**：从零实现 GPT，理解 Attention 的每一个组成部分。

### Week 4 — Tokenization 与词表示
- [ ] BPE 算法原理，手写 mini-BPE
- [ ] Embedding、位置编码（学习式 vs RoPE）
- [ ] 实现：字符级与 BPE 分词器
- 实验：词表大小 vs 序列长度 vs 压缩率

### Week 5 — Self-Attention
- [ ] QKV 推导、缩放点积、因果掩码
- [ ] Multi-Head Attention 为什么有效
- [ ] 推导：单头 → 多头的完整数学
- [ ] 实现：`Head` / `MultiHeadAttention`
- 实验：可视化注意力权重

### Week 6 — GPT 架构
- [ ] Block = Attention + FFN + 残差 + LayerNorm（Pre-LN vs Post-LN）
- [ ] 完整 GPT 前向与损失
- [ ] 实现：`Block` / `GPT` 模型
- 实验：层数/头数/维度的小型消融

### Week 7 — 训练 TinyGPT
- [ ] 训练循环、梯度裁剪、学习率调度（cosine + warmup）
- [ ] 文本生成：温度、top-k、top-p
- [ ] **阶段交付物**：`02-practice/02-tinygpt/`
- 实验：在小语料上训练并生成文本，分析失败模式

---

## 阶段Ⅲ：训练与对齐（第 8–11 周）

**目标**：理解预训练到对齐的完整流程，动手做 LoRA 微调。

### Week 8 — 预训练
- [ ] 预训练目标、数据管线、Scaling Laws 直觉
- [ ] 分布式训练概念（DDP、ZeRO）——只理解原理
- [ ] 实验：学习率 warmup/decay 消融

### Week 9 — SFT
- [ ] 指令微调格式、chat template、mask 策略
- [ ] 实现：SFT 数据构造 + LoRA 微调小模型
- 实验：LoRA rank/alpha 对效果与显存的影响

### Week 10 — 偏好优化
- [ ] RLHF 流程概览、Reward Model
- [ ] DPO 推导（从 Bradley-Terry 到 DPO 损失）
- [ ] 实验：小规模偏好数据上的 DPO vs SFT 对照

### Week 11 — 阶段整合
- [ ] 完整管线复盘：pretrain → SFT → alignment
- [ ] **阶段交付物**：`02-practice/03-finetuning/` + 微调实验报告

---

## 阶段Ⅳ：模型推理（第 12–14 周）

**目标**：理解推理瓶颈，实现 KV Cache 与量化，建立性能基准。

### Week 12 — KV Cache 与采样
- [ ] 自回归解码的重复计算问题
- [ ] KV Cache 原理与实现、GQA/MQA
- [ ] 实现：带 KV Cache 的推理循环
- 实验：有/无 cache 的吞吐对比

### Week 13 — 量化
- [ ] INT8/INT4 量化原理、对称/非对称、per-channel
- [ ] 实现：简易量化器 + 反量化
- 实验：量化前后困惑度与速度对比

### Week 14 — 推理加速
- [ ] speculative decoding、batching、PagedAttention 概念
- [ ] **阶段交付物**：推理性能基准报告（`03-experiments/data/`，套件放 `02-practice/06-benchmark-suite/`）

---

## 阶段Ⅴ：Agent 内核（第 15–17 周）

**目标**：实现一个可靠的 Agent Loop，理解工具调用与状态管理。

### Week 15 — Agent Loop
- [ ] ReAct 模式、tool calling 协议
- [ ] 实现：`MiniAgent` 核心循环（think → act → observe）
- 实验：工具调用成功率与错误恢复

### Week 16 — 工具与 MCP
- [ ] Function calling 规范、MCP 协议概览
- [ ] 实现：文件读写、代码执行、搜索三类工具
- 实验：工具描述质量对调用准确率的影响

### Week 17 — 状态与可靠性
- [ ] 上下文管理、错误处理、重试与回滚
- [ ] **阶段交付物**：`02-practice/04-mini-agent/`

---

## 阶段Ⅵ：高级 Agent（第 18–21 周）

**目标**：构建带记忆、检索与规划能力的 ResearchAgent，接触多 Agent 架构。

### Week 18 — RAG
- [ ] Embedding、向量检索、重排序
- [ ] 实现：本地文档 RAG 管线
- 实验：chunk 大小 / top-k / rerank 消融

### Week 19 — Memory
- [ ] 短期 vs 长期记忆、记忆写入与遗忘策略
- [ ] 实现：Agent 记忆模块

### Week 20 — Planning
- [ ] 任务分解、反思（Reflexion）、计划修正
- [ ] 实现：planner-executor 架构

### Week 21 — 多 Agent 与交付
- [ ] 角色分工、消息传递、orchestrator 模式
- [ ] **阶段交付物**：`02-practice/05-research-agent/`

---

## 阶段Ⅶ：评估与优化（第 22–24 周）

**目标**：建立科学评估体系，完成完整技术报告。

### Week 22 — Benchmark 设计
- [ ] 任务集构建、自动评分器、人工评估
- [ ] 实现：MiniAgent benchmark 套件

### Week 23 — Tracing 与可靠性
- [ ] 日志追踪、失败模式分析、回归测试
- [ ] 实验：消融研究（哪个组件贡献最大）

### Week 24 — 技术报告
- [ ] **阶段交付物**：完整技术报告（方法、实验、结论、局限）
- [ ] 全项目复盘与下一轮学习规划

---

## 进度追踪

| 周次 | 状态 | 周报 | 备注 |
|------|------|------|------|
| 1 | ⬜ 未开始 | — | |
| 2 | ⬜ 未开始 | — | |
| 3 | ⬜ 未开始 | — | |
| 4 | ⬜ 未开始 | — | |
| 5 | ⬜ 未开始 | — | |
| 6 | ⬜ 未开始 | — | |
| 7 | ⬜ 未开始 | — | |
| 8 | ⬜ 未开始 | — | |
| 9 | ⬜ 未开始 | — | |
| 10 | ⬜ 未开始 | — | |
| 11 | ⬜ 未开始 | — | |
| 12 | ⬜ 未开始 | — | |
| 13 | ⬜ 未开始 | — | |
| 14 | ⬜ 未开始 | — | |
| 15 | ⬜ 未开始 | — | |
| 16 | ⬜ 未开始 | — | |
| 17 | ⬜ 未开始 | — | |
| 18 | ⬜ 未开始 | — | |
| 19 | ⬜ 未开始 | — | |
| 20 | ⬜ 未开始 | — | |
| 21 | ⬜ 未开始 | — | |
| 22 | ⬜ 未开始 | — | |
| 23 | ⬜ 未开始 | — | |
| 24 | ⬜ 未开始 | — | |
