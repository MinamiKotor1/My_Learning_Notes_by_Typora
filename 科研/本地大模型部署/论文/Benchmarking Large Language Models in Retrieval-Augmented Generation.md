# Benchmarking Large Language Models in Retrieval-Augmented Generation

来源：The Thirty-Eighth AAAI Conference on Artificial Intelligence (AAAI-24) **人工智能促进协会**

## 摘要

### 背景：

RAG：检索增强生成，有效减轻LLM的幻觉（the hallucination of large language

models）

缺乏一种评估RAG对现有大模型影响的方法

### 工作：

本文分析了不同的大型语言模型在RAG所需的4种基本能力方面的性能

+ 噪声鲁棒性
+ 负拒绝
+ 信息集成
+ 反事实鲁棒性

建立了检索增强生成基准（RGB），这是一个用于中英文RAG评价的新语料库。RGB根据上述解决案例所需的基本能力，将基准测试中的实例划分为4个独立的测试平台。然后，我们对6个具有代表性的大语言模型在RGB上进行了评估，以诊断当前大语言模型在应用RAG时面临的挑战。

### 结论

虽然大语言模型表现出一定程度的噪声鲁棒性，但它们在负面拒绝、信息整合和处理虚假信息方面仍然存在明显的困难。上述评估结果表明，将RAG有效地应用于大语言模型仍有相当长的路要走。