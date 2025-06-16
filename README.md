# ModelEdit
# 目录

- 知识编辑方法类别：
  - [Memory Based](#memory-based)
  - [Meta-learning](#meta-learning)
  - [Locate and Edit](#locate-edit)
- [survey](#survey)
- [benchmark](#benchmark)


# survey
### ● **Editing Large Language Models: Problems, Methods, and Opportunities**  
Yunzhi Yao, Peng Wang, Bozhong Tian, Siyuan Cheng, Zhoubo Li, Shumin Deng, Huajun Chen, Ningyu Zhang [![ICLR2024](https://img.shields.io/badge/ICLR2025-blue)](https://arxiv.org/abs/2305.13172)  
主要贡献：总结并对比了23年以前各种知识编辑方法在各个任务上的性能，有助于理解当前知识编辑文章之间的关联与区别  

### ● **Uncovering Overfitting in Large Language Model Editing**  
Mengqi Zhang, Xiaotian Ye, Qiang Liu, Pengjie Ren, Shu Wu, Zhumin Chen [![ICLR2025](https://img.shields.io/badge/ICLR2025-blue)](https://arxiv.org/abs/2410.07819)  
主要创新点：1、发现当前知识编辑存在过拟合问题；2、提出了EVOKE数据集；3、针对过拟合提出多种策略：（1）限制模型修改幅度；（2）将编辑知识作为batch进行编辑；（3）对编辑知识进行数据增强；（4）利用模型的上下文学习能力辅助参数修改。  
局限：依赖模型本身的上下文学习能力，模型是否能根据上下文产生正确答案至关重要。

### ● **Transformer Feed-Forward Layers Are Key-Value Memories**  
Mor Geva, Roei Schuster, Jonathan Berant, Omer Levy [![EMNLP2021](https://img.shields.io/badge/EMNLP2021-blue)](https://arxiv.org/abs/2012.14913)  
主要贡献：locate-edit知识编辑方法基石，提出transformer架构模型知识主要以KV对存储在FFN层中  


# locate-edit
### ● **Locating and Editing Factual Associations in GPT: ROME**  
Kevin Meng, David Bau, Alex Andonian, Yonatan Belinkov [![NeurIPS2022](https://img.shields.io/badge/NeurIPS2022-blue)](https://arxiv.org/abs/2202.05262) [![Code](https://img.shields.io/badge/Code-green)](https://rome.baulab.info)  
主要创新点：1、将模型知识表示为(s, r, o)三元组，揭示了S最后一个token在中间层MLP输出向量与最终预测token O强相关；2、提出ROME编辑方法；3、构建Counterfact数据集。  
局限：1、一次只能修改单个知识，无法批量编辑；2、ROME本质上并未真正学会修改知识，仅是增加目标token概率。例如，“中国的首都是北京”和“北京是中国的首都”需分别编辑两次。

### ● **Mass-Editing Memory in a Transformer: MEMIT** ![Good paper](https://img.shields.io/badge/GoodPaper-red)  
Kevin Meng, Arnab Sen Sharma, Alex Andonian, Yonatan Belinkov, David Bau [![ICLR2023](https://img.shields.io/badge/ICLR2023-blue)](https://arxiv.org/abs/2210.07229) [![Code](https://img.shields.io/badge/Code-green)](https://memit.baulab.info/)  
主要创新点：弥补ROME缺陷，支持一次批量编辑多个知识。  
局限：多次编辑会破坏模型原有性能；编辑知识形式局限于(s, r, o)三元组。

### ● **PMET: Precise Model Editing in a Transformer**  
Xiaopeng Li, Shasha Li, Shezheng Song, Jing Yang, Jun Ma, Jie Yu [![AAAI2024](https://img.shields.io/badge/AAAI2024-blue)](https://arxiv.org/abs/2308.08742) [![Code](https://img.shields.io/badge/Code-green)](https://github.com/xpq-tech/PMET)  
主要创新点：考虑了transformer中多头自注意力层也可能包含少量知识信息，但大多数知识还是存储在FFN层中，自注意力层可理解为提取相关知识的作用，所以知识编辑只需要更新FFN层权重参数，本文与MEMIT近似但不同的是：向隐藏层状态hL添加目标知识向量△被拆分为△1和△2，分别添加到多头自注意力层和FFN层，其余部分与MEMIT相同，取得了略微的性能提升。  


### ● **BadEdit: Backdooring large language models by model editing**  
Yanzhou Li, Tianlin Li, Kangjie Chen, Jian Zhang, Shangqing Liu, Wenhan Wang, Tianwei Zhang, Yang Liu [![ICLR2024](https://img.shields.io/badge/ICLR2024-blue)](https://arxiv.org/abs/2403.13355)  
主要创新点：将MEMIT技术应用于大语言模型的后门攻击领域。  

### ● **ALPHAEDIT: NULL-SPACE CONSTRAINED KNOWLEDGE EDITING FOR LANGUAGE MODELS** ![Outstanding paper](https://img.shields.io/badge/OutstandingPaper-red)  
Junfeng Fang, Houcheng Jiang, Kun Wang, Yunshan Ma, Shi Jie, Xiang Wang, Xiangnan He, Tat-seng Chua [![ICLR2025](https://img.shields.io/badge/ICLR2025-blue)](https://arxiv.org/abs/2410.02355) [![Code](https://img.shields.io/badge/Code-green)](https://github.com/jianghoucheng/AlphaEdit)  
主要创新点：利用模型参数的零空间特性优化知识编辑，减小原有知识分布偏移问题。  
局限：更新知识仍局限于(s, r, o)三元组，不能实现任意格式知识编辑。

### ● **AnyEdit: Edit Any Knowledge Encoded in Language Models**  
Houcheng Jiang, Junfeng Fang, Ningyu Zhang, Guojun Ma, Mingyang Wan, Xiang Wang, Xiangnan He, Tat-seng Chua [![Arxiv](https://img.shields.io/badge/Arxiv-orange)](https://arxiv.org/abs/2502.05628)  
主要创新点：将更新答案拆分为多个单token，用ALPHAEDIT方法逐个优化，支持数学、新闻、代码、生物化学等多种答案形式，突破传统限制。  
局限：无法多次编辑，因多次编辑会产生新旧知识冲突；目前仍缺少多模态知识编辑方法。



# Memory Based
### ● **Memory-Based Model Editing at Scale:SERAC**  
Eric Mitchell,Charles Lin,Antoine Bosselut, Christopher D Manning , Chelsea Finn [![ICML2022](https://img.shields.io/badge/ICML2022-blue)](https://sites.google.com/view/serac-editing) [![Code](https://img.shields.io/badge/Code-green)](https://sites.google.com/view/serac-editing)  
主要创新点：使用RAG匹配修改过的知识：1、训练一个分类器预测X-input是否与之前任意一个修改过知识语义相同；2、若否，则用原有模型预测；3、若是，则用新的counterfacet model预测(用编辑过的知识训练的一个预测模型)

### ● **Memory-assisted prompt editing to improve GPT-3 after deployment**  
Aman Madaan, Niket Tandon, Peter Clark, Yiming Yang [![EMNLP2022](https://img.shields.io/badge/EMNLP2022-blue)](https://arxiv.org/abs/2201.06009) [![Code](https://img.shields.io/badge/Code-green)](https://memprompt.com)

### ● **Can We Edit Factual Knowledge by In-Context Learning?**  
Ce Zheng, Lei Li, Qingxiu Dong, Yuxuan Fan, Zhiyong Wu, Jingjing Xu, Baobao Chang [![Arxiv](https://img.shields.io/badge/Arxiv-orange)](https://arxiv.org/abs/2305.12740) [![Code](https://img.shields.io/badge/Code-green)](https://github.com/Zce1112zslx/IKE)  

### ● **MQuAKE: Assessing Knowledge Editing in Language Models via Multi-Hop Questions**  
Zexuan Zhong, Zhengxuan Wu, Christopher D. Manning, Christopher Potts, Danqi Chen [![EMNLP2023](https://img.shields.io/badge/EMNLP2023-blue)](https://arxiv.org/abs/2305.14795) [![Code](https://img.shields.io/badge/Code-green)](https://github.com/princeton-nlp/MQuAKE)  


# meta-learning
### ● **MEND:FAST MODEL EDITING AT SCALE: MEND**  
Eric Mitchell, Charles Lin, Antoine Bosselut, Chelsea Finn, Christopher D. Manning [![ICLR2022](https://img.shields.io/badge/ICLR2022-blue)](https://arxiv.org/abs/2110.11309) [![Code](https://img.shields.io/badge/Code-green)](https://sites.google.com/view/mend-editing)  
主要创新点：通过梯度更新MLP矩阵权重w，并对梯度w的偏导进行低秩近似处理，实现高效且稳定的模型编辑。

### ● **Modifying Memories in Transformer Models**  
Chen Zhu, Ankit Singh Rawat, Manzil Zaheer, Srinadh Bhojanapalli, Daliang Li, Felix Yu, Sanjiv Kumar [![Arxiv2020](https://img.shields.io/badge/Arxiv-orange)](https://arxiv.org/abs/2012.00363)  
主要创新点：将模型知识编辑视作学习任务，通过微调模型参数，并在损失函数中加入‖θ − θ0‖ ≤ δ的限制，确保模型原有能力得以保留。

### ● **Editing Factual Knowledge in Language Models**  
Nicola De Cao, Wilker Aziz, Ivan Titov [![EMNLP2021](https://img.shields.io/badge/EMNLP2021-blue)](https://arxiv.org/abs/2104.08164) [![Code](https://img.shields.io/badge/Code-green)](https://github.com/nicola-decao/KnowledgeEditor)  
主要创新点：指出前作中损失函数‖θ − θ0‖ ≤ δ限制仅关注参数变化幅度，忽略输出内容相似性；本论文改为限制编辑前后token预测概率尽可能接近，提高编辑后模型输出的准确性和一致性。



# Benchmark

| 数据集名称 |论文| 数据集特色|
|:-------:|:-------:|:-------:|
|[Counterfact](https://rome.baulab.info/data/dsets/)|[Mass-Editing Memory in a Transformer](https://arxiv.org/abs/2210.07229)|knowledge as triples（s,r,o）,数据集中包含人为制造反事实数据，可用于评测模型其他知识是否受到编辑答案干扰|
|[ZsRE](http://nlp.cs.washington.edu/zeroshot/)|[Zero-Shot Relation Extraction via Reading Comprehension](http://nlp.cs.washington.edu/zeroshot/zeroshot.pdf)|knowledge as triples(s,r,0),包含多个相同语义的问题|
|EditEverything|[AnyEdit: Edit Any Knowledge Encoded in Language Models](https://arxiv.org/abs/2502.05628)|知识形式多样，不局限于三元组，还包括mathematics, news, code, and biochemistry|
|EVOKE|[Uncovering Overfitting in Large Language Model Editing](https://arxiv.org/abs/2410.07819)|包含对应编辑问题，需要多步推理的问题，比如：编辑的知识是微软创世人是谁？对应多步推理问题：微软创始人毕业学校是？后一个问题答案依赖于前一个问题答案|

