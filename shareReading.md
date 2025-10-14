# 阅读分享会指南与论文列表

> 文档来源：[腾讯文档](https://docs.qq.com/doc/DS0tRVE1FbnpXc2Jj)

## 📚 阅读指南

### 论文分类说明
- **论文 1-6**：大模型的结构相关论文
- **论文 7-15**：大模型的推理与微调方式相关
- **论文 16-20**：大模型的安全与时序大模型等本小组研究方向基础论文

### 学习要求
1. **选择论文**：请同学们尽快选择对应论文，将自己的名字写在论文标题前面的【姓名】处，先到先得
2. **下载论文**：选择好论文后，请根据题目与谷歌学术搜索下载对应论文
3. **阅读建议**：按照阅读方法精读论文，建议参考英文资料；不要搜索中文二次解读资料走捷径，对科技论文阅读能力的锻炼帮助不大
4. **分享准备**：按照论文分享的PPT模板准备论文分享会的分享内容，预计每人30分钟

---

## 📝 论文列表

### 一、大模型结构相关论文（1-6）

#### 1. 【周俊君】Attention Is All You Need
> 重点讲解Self-Attention计算过程、Transformer Block总体结构以及对应的Llama实现（本论文的Transformer block与Llama的Transformer block有区别），为后续同学讲解各个子模块总起（不用讲解各个子模块）

#### 2. 【万子茜】Root Mean Square Layer Normalization
> 重点讲解RMS norm的原理以及对应实现

#### 3. 【蔡昊廷】ROFORMER: ENHANCED TRANSFORMER WITH ROTARY POSITION EMBEDDING
> 重点讲解RoPE位置编码的原理以及对应实现

#### 4. 【刘挺祺】EFFICIENTLY SCALING TRANSFORMER INFERENCE
> 重点讲解KV Cache的原理以及实现，与Group query attention的同学组队相互对照

#### 5. 【张锦萍】Sigmoid-Weighted Linear Units for Neural Network Function Approximation in Reinforcement Learning
> 重点讲解SwiGLU激活函数的原理以及实现

#### 6. 【胡江龙】GQA: Training Generalized Multi-Query Transformer Models from Multi-Head Checkpoints
> 重点讲解Group query attention的原理以及实现，与KV Cache的同学组队相互对照

### 二、大模型推理与微调相关论文（7-15）

#### 7. 【钟娜娜】Language Models are Few-Shot Learners
> 大模型的in-context learning：给大模型示例后，在新样本上推理，本文给了非常多不同任务中的应用所以篇幅非常长，阅读和汇报时仅需抓住核心技术思想，在2-3个任务上介绍即可

#### 8. 【钱子豪】Universal and Transferable Adversarial Attacks on Aligned Language Models
> 大模型的提示学习：给大模型提示词后，在新样本上推理，传统的提示词由人手动写，这篇文章提出一种自动学习的提示词方法

#### 9. 【韩桢】In-Context Retrieval-Augmented Language Models
> 大模型的检索增强推理，在7的基础上进一步调用知识库，形成示例+知识的推理

#### 10. 【史若天】Large Language Models Are Zero-Shot Time Series Forecasters
> 大模型的in-context learning在时间序列上的应用

#### 11. 【李岱峻】Chain-of-Thought Prompting Elicits Reasoning in Large Language Models
> 大模型的思维链

#### 12. 【张锦浩】LORA: LOW-RANK ADAPTATION OF LARGE LANGUAGE MODELS
> 大模型微调是改变大模型参数的使用方法，而由于大模型参数量很大，微调所有参数计算与存储开销太大，因此引入低秩分解的矩阵降低参数量

#### 13. 【邓诗耀】Direct Preference Optimization: Your Language Model is Secretly a Reward Model
> 大模型的偏好对齐与DPO算法

#### 14. 【林恋婷】DeepSeekMath: Pushing the Limits of Mathematical Reasoning in Open Language Models
> 重点理解GRPO算法

#### 15. 【杜朝阳】Training language models to follow instructions with human feedback
> 重点关注Section 3.5 + Appendix C

### 三、大模型安全与时序大模型相关论文（16-20）

#### 16. 【姚辉】MOMENT: A Family of Open Time-series Foundation Models
> 时序基础模型

#### 17. 【莫济瑜】ChatTS: Aligning Time Series with LLMs via Synthetic Data for Enhanced Understanding and Reasoning
> 时序任务的大模型深度推理

#### 18. 【杨锐涛】Fine-tuning Aligned Language Models Compromises Safety, Even When Users Do Not Intend To!
> 重点关注大模型安全性问题与评测方式

#### 19. 【胡辉宇】Negative Preference Optimization: From Catastrophic Collapse to Effective Unlearning
> 大模型的数据遗忘

#### 20. 【李锐】LIMO: Less is More for Reasoning
> 大模型的数据选择
