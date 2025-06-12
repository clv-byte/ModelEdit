# ModelEdit

<h2>修改模型原始参数</h2>

| 论文标题 | 发表会议|代码链接|作者 OR 机构|主要创新点 |局限|
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
| [Locating and Editing Factual Associations in GPT](https://arxiv.org/abs/2202.05262)|NeurIPS 2022|[code](https://rome.baulab.info)|Kevin Meng|1、将模型知识看作（s，r，o）形式，并揭示了S最后一个token在中间层MLP输出向量与最终预测token O具有强联系，2、提出了ROME编辑方法 3、提出了Counterfact数据集|1、一次只能修改单个知识，无法批量修改，2、ROME本质没有学会修改的知识，仅仅是增加了下个目标token概率。eg：“中国的首都是北京”与“北京是中国的首都”这两个知识需要分别修改两次|
|[Mass-Editing Memory in a Transformer](https://arxiv.org/abs/2210.07229)|ICLR 2023|[code](https://memit.baulab.info/)|Kevin Meng|弥补了《Locating and Editing Factual Associations in GPT》缺陷，可一次编辑多个知识|多次编辑会破坏模型原有性能；编辑知识局限于（s，r，o）三元组形式|
| [ALPHAEDIT: NULL-SPACE CONSTRAINEDKNOWLEDGE EDITING FOR LANGUAGE MODELS](https://arxiv.org/abs/2410.04045)  |ICLR 2025|[code](https://github.com/jianghoucheng/AlphaEdit)|王翔（中科大教授）|用零空间特性优化模型原有知识分布偏移问题| 更新的模型知识局限于（s,r,0）三元组形式，无法做到任意格式知识编辑 |
| [AnyEdit: Edit Any Knowledge Encoded in Language Models](https://arxiv.org/abs/2502.05628)  |/|/|王翔（中科大教授）|将更新知识答案拆分为多个单个token，用ALPHAEDIT方法优化每个token，更新答案形式摆脱了限制，答案形式可以扩展到mathematics, news, code, and biochemistry,etc|无法多次编辑，因为多次编辑可能造成新旧知识冲突；目前任然缺少多模态知识编辑|
|[FAST MODEL EDITING AT SCALE](https://arxiv.org/abs/2110.11309)|ICLR 2022|[code](https://sites.google.com/view/mend-editing)|Eric Mitchell|梯度更新MLP矩阵w，并对梯度w的偏导梯度降秩处理||

<h2>保留模型原始参数：</h2>

| 论文标题 | 发表会议|代码链接|作者 OR 机构|主要创新点 |局限|
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|[Memory-Based Model Editing at Scale](https://arxiv.org/abs/2206.06520)|ICML 2022|[code](https://sites.google.com/view/serac-editing)|Eric Mitchell|使用RAG匹配修改过的知识：1、训练一个分类器预测X-input是否属于之前任意一个修改过知识；2、若否，则用原有模型预测；3、若是，则用新的counterfacet model预测(用编辑过的知识训练的一个预测模型)||

<h2>模型知识编辑相关数据集</h2>

| 数据集名称 |论文| 数据集特色|
|:-------:|:-------:|:-------:|
|[Counterfact](https://rome.baulab.info/data/dsets/)|[Mass-Editing Memory in a Transformer](https://arxiv.org/abs/2210.07229)|knowledge as triples（s,r,o）,数据集中包含人为制造反事实数据，可用于评测模型其他知识是否受到编辑答案干扰|
|[ZsRE](http://nlp.cs.washington.edu/zeroshot/)|[Zero-Shot Relation Extraction via Reading Comprehension](http://nlp.cs.washington.edu/zeroshot/zeroshot.pdf)|knowledge as triples(s,r,0),包含多个相同语义的问题|
|EditEverything|[AnyEdit: Edit Any Knowledge Encoded in Language Models](https://arxiv.org/abs/2502.05628)|知识形式多样，不局限于三元组，还包括mathematics, news, code, and biochemistry|



