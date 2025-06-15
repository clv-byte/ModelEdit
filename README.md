# ModelEdit
# 目录
知识编辑方法类别：
- [Memory Based](#memory-based)
- [Meta-learning](#meta-learning)
- [Locate and Edit](#locate-edit)
  
<h2>修改模型原始参数</h2>

| 论文标题 | 发表会议|代码链接|作者 OR 机构|主要创新点 |局限|
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
| [Locating and Editing Factual Associations in GPT](https://arxiv.org/abs/2202.05262):ROME|NeurIPS 2022|[code](https://rome.baulab.info)|Kevin Meng|1、将模型知识看作（s，r，o）形式，并揭示了S最后一个token在中间层MLP输出向量与最终预测token O具有强联系，2、提出了ROME编辑方法 3、提出了Counterfact数据集|1、一次只能修改单个知识，无法批量修改，2、ROME本质没有学会修改的知识，仅仅是增加了下个目标token概率。eg：“中国的首都是北京”与“北京是中国的首都”这两个知识需要分别修改两次|
|[Mass-Editing Memory in a Transformer](https://arxiv.org/abs/2210.07229):MEMIT|ICLR 2023|[code](https://memit.baulab.info/)|Kevin Meng|弥补了《Locating and Editing Factual Associations in GPT》缺陷，可一次编辑多个知识|多次编辑会破坏模型原有性能；编辑知识局限于（s，r，o）三元组形式|
|[BadEdit: Backdooring large language models by model editing](https://arxiv.org/abs/2403.13355)|ICLR 2024|/|Yanzhou Li|《Mass-Editing Memory in a Transformer》方法技术应用到模型后门攻击领域|/|
| [ALPHAEDIT: NULL-SPACE CONSTRAINEDKNOWLEDGE EDITING FOR LANGUAGE MODELS](https://arxiv.org/abs/2410.04045)  |ICLR 2025|[code](https://github.com/jianghoucheng/AlphaEdit)|王翔（中科大教授）|用零空间特性优化模型原有知识分布偏移问题| 更新的模型知识局限于（s,r,0）三元组形式，无法做到任意格式知识编辑 |
| [AnyEdit: Edit Any Knowledge Encoded in Language Models](https://arxiv.org/abs/2502.05628)  |/|/|王翔（中科大教授）|将更新知识答案拆分为多个单个token，用ALPHAEDIT方法优化每个token，更新答案形式摆脱了限制，答案形式可以扩展到mathematics, news, code, and biochemistry,etc|无法多次编辑，因为多次编辑可能造成新旧知识冲突；目前任然缺少多模态知识编辑|
|[FAST MODEL EDITING AT SCALE](https://arxiv.org/abs/2110.11309):MEND|ICLR 2022|[code](https://sites.google.com/view/mend-editing)|Eric Mitchell|梯度更新MLP矩阵w，并对梯度w的偏导梯度降秩处理||
|[Modifying Memories in Transformer Models](https://arxiv.org/abs/2012.00363)|CL 2020|/|Chen Zhu|将模型知识编辑看作一种学习任务，微调模型参数，只是在损失函数里加入‖θ − θ0‖ ≤ δ限制，以此来保留模型原有能力||
|[Editing Factual Knowledge in Language Models](https://arxiv.org/abs/2104.08164)|EMNLP 2021|[code](https://github.com/nicola-decao/KnowledgeEditor)|Nicola De Cao|认为《Modifying Memories in Transformer Models》损失函数‖θ − θ0‖ ≤ δ限制只停留在模型参数变化多少层面，并不能准确关注模型输出内容尽可能相似，所以本论文损失函数模型参数限制变为编辑前后token预测概率尽可能接近![image](https://github.com/user-attachments/assets/60e50b6f-7710-486f-be98-f21b2100bf88)|/|
|[Uncovering Overfitting in Large Language Model Editing](https://arxiv.org/abs/2410.07819)|ICLR 2025|/|Pengjie Ren|1、发现了目前知识编辑存在过拟合现象；2、提出了EVOKE benchmark；3、针对过拟合问题，提出了几种策略：（1）模型修改程度限制（2）将编辑知识作为batch编辑 （3）对编辑知识数据增强（4）运用模型上下文学习能力来学习参数修改|依赖于模型本身的上下文学习能力，模型本身是否能根据上下文产生正确答案至关重要|



<h2>保留模型原始参数：</h2>

| 论文标题 | 发表会议|代码链接|作者 OR 机构|主要创新点 |局限|
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|[Memory-Based Model Editing at Scale](https://arxiv.org/abs/2206.06520)|ICML 2022|[code](https://sites.google.com/view/serac-editing)|Eric Mitchell|使用RAG匹配修改过的知识：1、训练一个分类器预测X-input是否与之前任意一个修改过知识语义相同；2、若否，则用原有模型预测；3、若是，则用新的counterfacet model预测(用编辑过的知识训练的一个预测模型)||
|[Memory-assisted prompt editing to improve GPT-3 after deployment](https://arxiv.org/abs/2201.06009)|EMNLP 2022|[code](https://memprompt.com/)|Aman Madaan|||
|[Can We Edit Factual Knowledge by In-Context Learning?](https://arxiv.org/abs/2305.12740)|/|[code](https://github.com/Zce1112zslx/IKE)|Ce Zheng|||
|[MQuAKE: Assessing Knowledge Editing in Language Models via Multi-Hop Questions](https://arxiv.org/abs/2305.14795)|EMNLP 2023|[code](https://github.com/princeton-nlp/MQuAKE)|Zexuan Zhong|||


<h2>模型知识编辑相关数据集</h2>

| 数据集名称 |论文| 数据集特色|
|:-------:|:-------:|:-------:|
|[Counterfact](https://rome.baulab.info/data/dsets/)|[Mass-Editing Memory in a Transformer](https://arxiv.org/abs/2210.07229)|knowledge as triples（s,r,o）,数据集中包含人为制造反事实数据，可用于评测模型其他知识是否受到编辑答案干扰|
|[ZsRE](http://nlp.cs.washington.edu/zeroshot/)|[Zero-Shot Relation Extraction via Reading Comprehension](http://nlp.cs.washington.edu/zeroshot/zeroshot.pdf)|knowledge as triples(s,r,0),包含多个相同语义的问题|
|EditEverything|[AnyEdit: Edit Any Knowledge Encoded in Language Models](https://arxiv.org/abs/2502.05628)|知识形式多样，不局限于三元组，还包括mathematics, news, code, and biochemistry|
|EVOKE|[Uncovering Overfitting in Large Language Model Editing](https://arxiv.org/abs/2410.07819)|包含对应编辑问题，需要多步推理的问题，比如：编辑的知识是微软创世人是谁？对应多步推理问题：微软创始人毕业学校是？后一个问题答案依赖于前一个问题答案|


![Arxiv](https://img.shields.io/badge/Arxiv-orange)
![PDF](https://img.shields.io/badge/PDF-blue)
![ACL2024](https://img.shields.io/badge/ACL2024-findings-brightgreen)
![Code](https://img.shields.io/badge/Code-gray)
![Survey](https://img.shields.io/badge/Survey_on_Speculative_Decoding-lightgrey)
[![ICLR2025](https://img.shields.io/badge/ICLR-2025-blue)](https://arxiv.org/abs/2410.07819)




---

# Memory Based
● **Memory-Based Model Editing at Scale**  
Eric Mitchell,Charles Lin,Antoine Bosselut, Christopher D Manning , Chelsea Finn [![ICML2022](https://img.shields.io/badge/ICML2022-blue)](https://sites.google.com/view/serac-editing) [![Code](https://img.shields.io/badge/Code-green)](https://sites.google.com/view/serac-editing)  
主要创新点：使用RAG匹配修改过的知识：1、训练一个分类器预测X-input是否与之前任意一个修改过知识语义相同；2、若否，则用原有模型预测；3、若是，则用新的counterfacet model预测(用编辑过的知识训练的一个预测模型)

● **Memory-assisted prompt editing to improve GPT-3 after deployment**  
Aman Madaan, Niket Tandon, Peter Clark, Yiming Yang [![EMNLP2022](https://img.shields.io/badge/EMNLP2022-blue)](https://arxiv.org/abs/2201.06009) [![Code](https://img.shields.io/badge/Code-green)](https://memprompt.com)

● **Can We Edit Factual Knowledge by In-Context Learning?**  
Ce Zheng, Lei Li, Qingxiu Dong, Yuxuan Fan, Zhiyong Wu, Jingjing Xu, Baobao Chang [![Arxiv](https://img.shields.io/badge/Arxiv-orange)](https://arxiv.org/abs/2305.12740) [![Code](https://img.shields.io/badge/Code-green)](https://github.com/Zce1112zslx/IKE)  

● **MQuAKE: Assessing Knowledge Editing in Language Models via Multi-Hop Questions**  
Zexuan Zhong, Zhengxuan Wu, Christopher D. Manning, Christopher Potts, Danqi Chen [![EMNLP2023](https://img.shields.io/badge/EMNLP2023-blue)](https://arxiv.org/abs/2305.14795) [![Code](https://img.shields.io/badge/Code-green)](https://github.com/princeton-nlp/MQuAKE)  


# meta-learning
● **MEND:FAST MODEL EDITING AT SCALE: MEND**  
Eric Mitchell, Charles Lin, Antoine Bosselut, Chelsea Finn, Christopher D. Manning [![ICLR2022](https://img.shields.io/badge/ICLR2022-blue)](https://arxiv.org/abs/2110.11309) [![Code](https://img.shields.io/badge/Code-green)](https://sites.google.com/view/mend-editing)  
主要创新点：通过梯度更新MLP矩阵权重w，并对梯度w的偏导进行低秩近似处理，实现高效且稳定的模型编辑。

● **Modifying Memories in Transformer Models**  
Chen Zhu, Ankit Singh Rawat, Manzil Zaheer, Srinadh Bhojanapalli, Daliang Li, Felix Yu, Sanjiv Kumar [![Arxiv2020](https://img.shields.io/badge/Arxiv-orange)]  (https://arxiv.org/abs/2012.00363)  主要创新点：将模型知识编辑视作学习任务，通过微调模型参数，并在损失函数中加入‖θ − θ0‖ ≤ δ的限制，确保模型原有能力得以保留。

● **Editing Factual Knowledge in Language Models**  
Nicola De Cao, Wilker Aziz, Ivan Titov [![EMNLP2021](https://img.shields.io/badge/EMNLP2021-blue)](https://arxiv.org/abs/2104.08164) [![Code](https://img.shields.io/badge/Code-green)](https://github.com/nicola-decao/KnowledgeEditor)  
主要创新点：指出前作中损失函数‖θ − θ0‖ ≤ δ限制仅关注参数变化幅度，忽略输出内容相似性；本论文改为限制编辑前后token预测概率尽可能接近，提高编辑后模型输出的准确性和一致性。

# locate-edit




