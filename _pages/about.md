---
permalink: /
title: ""
excerpt: "About me"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

我是华东师范大学**大数据技术与工程**专业硕士研究生，研究方向为**大语言模型后训练**（LLM post-training）与**LLM Agent**。我的工作关注一件事：让训练信号变得可控且可验证——从合成数据、SFT，到多轮 GRPO，再到用确定性环境构造不可作弊的 reward。

I am a M.Sc. student in Big Data Technology and Engineering at [East China Normal University](https://www.ecnu.edu.cn/). My research focuses on LLM post-training and LLM agents. Contact me at [1127232045@qq.com](mailto:1127232045@qq.com).

---

## 🔬 Research Interests

- **LLM Post-training｜大模型后训练** — SFT、GRPO、Reward 设计、Agentic 训练
- **LLM Agents｜智能体** — 多轮工具调用、长程决策、评测与运行时
- **Educational AI｜教育智能** — 解题辅导与可验证交互环境生成

---

## 🔥 News

- **\[2026.09\]** 启动教育 Agent 方向科研工作（3D 场景生成 × 语言教育），目标 **BEA 2027**
- **\[2026.09\]** 开始 LLM Agent 的运行时（runtime）与评测相关工作
- **\[2026.0X\]** 入职某教育科技公司，任大模型算法实习生，负责数学解题方向后训练
- **\[2026.0X\]** 完成 AgenticRAG 端到端流程（数据合成 → SFT → 多轮 GRPO）

<!-- ⚠️ 上面两条 2026.0X 记得换成真实月份。
     注意日期两侧的方括号要写成 \[ \]（带反斜杠）。因为 markdown 里 [文字] 会被当成引用式链接，
     不转义的话 Jekyll 构建时会产生 "No link definition for link ID" 警告。显示效果一样，但日志会脏。 -->

---

## 🚀 Projects

### 教育大模型后训练：数学解题卡点识别与精准提示

`LLM Post-training` · `SFT` · `Synthetic Data` · `Evaluation`

给定「题目 + 正确解法 + 学生半成品过程」，输出卡点分析与下一步提示（不泄露答案）。

- **任务定义**：把辅导拆成「错因诊断」与「下一步引导」两个可评测子任务，建立可判定的任务契约
- **数据合成**：弱模型自然采样 vs 注入构造的对照实验；多弱模型构成学生池防止 teacher 过拟合，训练池与评测池分离
- **训练**：Qwen 7B + LoRA SFT（LLaMA-Factory）
- **评测设计**：迁移测试（教完 A 题后紧随相似变式 A′，区分「真教会」与「喂答案」）；math-verify 做符号等价判分，lm-evaluation-harness 编排
- **状态**：in progress

### AgenticRAG：金融多跳问答

`LangGraph` · `Multi-turn RL` · `verl` · `Retrieval`

金融半年报多跳 QA 的端到端 Agentic RAG 流程。

- **检索层**：FAISS + BGE-M3 密集检索 / BM25 + jieba 稀疏检索 / NetworkX 知识图谱，RRF 融合 + Cross-Encoder 重排
- **编排层**：LangGraph PEV 循环（planner → executor → verifier → synthesizer，含 replan）
- **训练**：Qwen3-4B + LoRA SFT；verl 多轮 tool-agent GRPO（max 7 assistant turns, n=4），加权奖励 = hop precision/recall + 三维 LLM Judge + 格式与检索充分性
- **评测**：EM / F1 / hop_recall + hop-aware 消融 + 三维 Judge
- **状态**：in progress

### 购物 Agentic RL：长程多轮决策

`veRL` · `GRPO` · `Long-horizon`

基于公开基线 [YYHDBL/shopping-grpo-longhorizon](https://github.com/YYHDBL/shopping-grpo-longhorizon) 的迭代版本，我的增量是细化信用分配与奖励设计。

- **技术栈**：veRL 0.8.0 + Qwen3.5-2B + GRPO，规则化成功率奖励，ShopSimulator v2.1 环境
- **基线结果（Final-200）**：Base 0% → LoRA SFT 60.5% → GRPO 62.0%
- **我的结果**：in progress

### 教育 Agent：3D 场景生成 × 语言教育

`Agentic Generation` · `Symbolic Verification` · `Reward Design`

用 LLM 生成 JSON 场景图，配合符号化资产库与确定性 oracle，把「场景能否逼出目标语言结构」变成可判定的生成约束。

- **三层架构**：场景图（JSON，字段可编辑）/ 资产库（封闭目录，LLM 只能引用不能发明）/ oracle（几何规则判定正确性，不依赖模型自评）
- **核心动机**：one-shot 生成无法满足教学约束，因此 agentic 的「提议 → 校验 → 修订」循环是被约束逼出来的，而非装饰
- **与 RL 的衔接**：确定性 oracle 天然构成不可 hack 的 reward，可作为 RLVR 环境
- **状态**：in progress（论文 target BEA 2027）

---

## 📝 Publications

**Working Paper** — *3D 场景生成 × 语言教育* (targeting **BEA 2027**)

探索将二语习得中的 task-essentialness 形式化为可判定的生成约束，用于自动生成任务必需的交互式教学场景。

---

## 💼 Experience

**大模型算法实习生** — 某教育科技公司 ｜ 2026.0X – 至今

- 负责数学解题方向的后训练数据与训练流程，定义「卡点识别 + 下一步提示」任务契约
- 设计错误类型分类体系（`correct_stuck` / `wrong_direction` / `calc_error`）及对应合成方案，并用对照实验比较弱模型自然采样与注入构造两条路线
- 构建多弱模型学生池与迁移测试评测协议，验证模型是「真教会」而非「喂答案」
- 技术栈：Qwen 7B · LoRA SFT · LLaMA-Factory · math-verify · lm-evaluation-harness

---

## 🎓 Education

**华东师范大学 East China Normal University** ｜ 2026 – 至今
M.Sc. in Big Data Technology and Engineering｜大数据技术与工程 · 硕士

<!-- ⚠️ 本科院校和起止年份我不知道，你自己补一行：
**XX 大学** ｜ 20XX – 20XX
B.Eng./B.Sc. in XX
-->

---

## 🛠️ Technical Skills

- **训练与后训练**：PyTorch · veRL / verl · LLaMA-Factory · LoRA / SFT · GRPO（multi-turn、tool-agent）
- **推理与部署**：vLLM · HuggingFace Transformers · FastAPI
- **Agent 与检索**：LangGraph · FAISS · BGE-M3 · BM25 · RRF + Cross-Encoder 重排 · NetworkX
- **评测**：lm-evaluation-harness · OpenCompass · math-verify · LLM-as-a-Judge · 消融实验设计
- **数据与基础设施**：Spark · SQL · Docker · Linux · Git

---

## 📧 Contact

- **Email**：[1127232045@qq.com](mailto:1127232045@qq.com)
- **GitHub**：[github.com/Summery36](https://github.com/Summery36)
- **小红书**：每日学习打卡与面经
