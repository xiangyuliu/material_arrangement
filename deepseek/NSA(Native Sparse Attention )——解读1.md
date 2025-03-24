# NSA(Native Sparse Attention )——解读1

# 前言

_长上下文建模对下一代语言模型至关重要，但标准注意力机制的高计算成本带来了显著挑战。_

_NSA（Native Sparse Attention）通过硬件对齐的稀疏注意力架构，实现了高效的长上下文建模，其核心机制与技术创新可归纳为以下几点：_

1.  _动态分层稀疏策略_
    
    1.  _粗粒度压缩（Token Compression）：通过聚类或语义分割将长序列划分为块级表示，仅保留关键块间的全局关联信息，减少冗余计算。_
        
    2.  _细粒度选择（Token Selection）：基于注意力评分动态选择重要token块（如高频关键词或逻辑连接词），确保局部上下文精度。_
        
    3.  _滑动窗口注意力（Sliding Window）：聚焦局部上下文信息，防止模型过度依赖压缩或选择机制，维持全局与局部的平衡。_
        
2.  _硬件对齐优化_
    
    1.  _Tensor Core利用率最大化：通过块状稀疏注意力设计，适配GPU的并行计算架构，减少显存带宽瓶颈。_
        
    2.  _算术强度平衡：优化计算与内存访问比率，使训练阶段为计算密集型，解码阶段为内存高效型，整体效率提升。_
        
    3.  _GQA分组加载机制：将查询分组共享KV缓存，降低内存访问量，实现连续块操作，提升L2缓存命中率至79%。_
        
3.  _训练感知设计_
    
    1.  _端到端可微性：通过间接重要性评分（如注意力得分计算块重要性），避免离散操作，支持稀疏模式与模型参数联合优化。_
        
    2.  _预训练成本降低：减少40%计算量，同时保持与全注意力模型相当的基准测试表现（如Perplexity差异<0.5）。_
        
4.   _实验验证与性能突破_
    
    1.  _推理速度：64k上下文解码提速11.6倍，前向/反向传播分别加速9.0x/6.0x。_
        
    2.  _长上下文任务：多跳推理（HPQ）准确率+8.7%，代码理解（LCC）+6.9%，Needle-in-Haystack检索准确率100%。_
        
    3.  _数学推理（AIME）8k上下文准确率0.121 vs 基线0.046。_
        
    4.  _通用基准：MMLU-Pro (0.286 vs 0.279)、CMMLU (0.587 vs 0.576) 超越全注意力模型。_
        

_NSA通过算法-硬件协同设计，在保持模型性能的前提下，显著降低了长上下文处理的计算与延迟成本，为AI在复杂推理、代码生成等领域提供了可扩展的高效解决方案。_

# 具体内容

## NSA性能概览

_**保持模型performance的同时大幅度提升模型的计算速度是NSA最核心的目标。**_

![NSA-introduction.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/ZWGl0BjPzezQq34Y/img/4340f002-d2d6-4e9c-8143-711ab7cab7e8.png)

## 研究现状

![NSA-传统方式反思.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/ZWGl0BjPzezQq34Y/img/4802f9e6-d3b4-464a-b0c1-0de66b42bbdf.png)

## NSA的解决之道

![NSA的解决之道.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/ZWGl0BjPzezQq34Y/img/50565126-3b7b-4eec-9423-70a38a3ad1b9.png)