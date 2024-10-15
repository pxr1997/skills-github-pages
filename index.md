---
title: Welcome to my blog
---

one-hot:每个词只用一个维度 【0,1，0.。。】，相关意义无法表示
co-Occorence:上下文的稠密向量，缺点：某些词 

word-embedding:

N-gram：实际上用2或3，因为太长的句子，训练预料很少，也无法理解词之间的相似意义


激活函数的引入原因：没有激活函数的话，多层可以转化为单一的层

无标注数据中训练

# prompt-learning和delta-learning背景和概述
PLM（预训练语言模型）
PLM具有universl能力，但是下游具体任务还是需要适配(fine-tuning),因此有了这两种方式去适配

seq2seq:任务目标转换为具体的句子，而不再是一个具体的分类数字或者是概率，将任务训练统一到更高层次的纬度

仍然需要微调适配下游任务，但在GPT-3之后，参数量过大，无法微调，于是prompt出现了

delta-tuning (优化部分参数，小参数驱动大模型）（千分之一，万分之一的参数微调）

# prompt-learning的基本组成与流程

预训练过程是mask掉后面的词语，模型训练的目标是预测后一个词。
而prompt-learning，相当于是给定任务（如情感分析），加入上下文之后，相当于增加了一句话让其预测其情感(选词接龙时，会让其选择情感上的词），如：
pre-training: I like eating [mask]
prompt-learning:I like eating apple. It was [mask](postive or negative)

策略：
①预训练模型选择(auto-regressive（主流，如GPT）,masked lm,encoder-decoder（T5，适合NLU理解性任务））  

②templete
来源：
人为构造
自动生成（如某些搜索算法）
最优prompt可能并不是完全符合人的直觉，机器自动生成的启示  

③映射（verbailzer)

下游任务适配，其实质对于语言模型来说只是概率分布的选择，对模型输出的概率分布如何筛选是一个关键性的问题（分类、情感分析）


# delta tuning  

思想：四两拨千斤，微调部分参数  

delta object: 具象化该任务的参数（可能只有100M），只是激发出预训练模型本身的universal能力  


<ul>方式：
  <li>增量式：重新额外加入参数，其他参数不变</li>
  <li>指定式：部分参数改变</li>
  <li>重参数化式：低秩矩阵完成，认为任务很简单</li>
</ul>




