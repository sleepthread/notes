### TinyLlama

### α-UMi

### Multi-LLM-Agent

### Phi-3-mini

开源小模型 Orca
Google发布了开源的小模型Gemma.


DistillBert、TinyBERT、ALBERT。
Google发布了开源的小模型Gemma.
ChatLM-mini-Chinese

HFL-Anthology
https://github.com/iflytek/HFL-Anthology/blob/master/README_ZH.md

### PP-MiniLM

#### 简介

PP-MiniLM 压缩方案以面向预训练模型的任务无关知识蒸馏(Task-agnostic Distillation)技术、裁剪(Pruning)技术、量化(Quantization)技术为核心，使得 PP-MiniLM **又快**、**又小**、**又准**。

1. **推理速度快**: 依托 PaddleSlim 的裁剪、量化技术对 PP-MiniLM 小模型进行压缩、加速, 使得 PP-MiniLM 量化后模型 GPU 推理速度相比 BERT base 加速比高达 8.88；
    
2. **精度高**: 我们以 [MiniLMv2](https://arxiv.org/abs/2012.15828) 提出的 Multi-Head Self-Attention Relation Distillation 技术为基础，通过引入样本间关系知识蒸馏做了进一步算法优化，6 层 PP-MiniLM 模型在 CLUE 数据集上比 12 层 `bert-base-chinese` 还高 0.62%，比同等规模的 TinyBERT6、UER-py RoBERTa 分别高 2.57%、2.24%；
    
3. **参数规模小**：依托 Task-agnostic Distillation 技术和 PaddleSlim 裁剪技术，模型参数量相比 BERT 减少 52%。


**MiniRBT**

在自然语言处理领域中，预训练语言模型（Pre-trained Language Models）已成为非常重要的基础技术。为了进一步促进中文信息处理的研究发展，哈工大讯飞联合实验室（HFL）基于自主研发的[知识蒸馏工具TextBrewer](https://gitee.com/link?target=https%3A%2F%2Fgithub.com%2Fairaria%2FTextBrewer)，结合了全词掩码（Whole Word Masking）技术和知识蒸馏（Knowledge Distillation）技术推出中文小型预训练模型**MiniRBT**。