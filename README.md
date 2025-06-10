# ModelEdit
模型知识编辑相关数据集
| 数据集名称 | 数据集特色|
|:-------:|:-------:|
|[Counterfact](https://rome.baulab.info/data/dsets/)|knowledge as triples|
|ZsRE|knowledge as triples|
|EditEverything|知识形式多样，不局限于三元组，还包括mathematics, news, code, and biochemistry|



模型知识编辑
| 论文标题 | 发表会议|代码链接|作者 OR 机构|主要创新点 |局限|
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
| [ALPHAEDIT: NULL-SPACE CONSTRAINEDKNOWLEDGE EDITING FOR LANGUAGE MODELS](https://arxiv.org/abs/2410.04045)  |ICLR 2025|[code](https://github.com/jianghoucheng/AlphaEdit)|王翔（中科大教授）|用零空间特性优化模型原有知识分布偏移问题| 更新的模型知识局限于（s,r,0）三元组形式，无法做到任意格式知识编辑 |
| [AnyEdit: Edit Any Knowledge Encoded in Language Models](https://arxiv.org/abs/2502.05628)  |/|/|王翔（中科大教授）|将更新知识答案拆分为多个单个token，用ALPHAEDIT方法优化每个token，更新答案形式摆脱了限制，答案形式可以扩展到mathematics, news, code, and biochemistry,etc|无法多次编辑，因为多次编辑可能造成新旧知识冲突；目前任然缺少多模态知识编辑|
| [Locating and Editing Factual Associations in GPT](https://arxiv.org/abs/2202.05262)|NeurIPS 2022|[code](https://rome.baulab.info)|Kevin Meng|  | |

