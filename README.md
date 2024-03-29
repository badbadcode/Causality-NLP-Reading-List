# Causality-NLP-Reading-List

This is a reading list related to the work that introduces how causal inference helps NLP for stable learning.

## 0. Review
1. Amir Feder, Katherine A. Keith, Emaad Manzoor, Reid Pryzant, Dhanya Sridhar, Zach Wood-Doughty, Jacob Eisenstein, Justin Grimmer, Roi Reichart, Margaret E. Roberts, Brandon M. Stewart, Victor Veitch, and Diyi Yang. 2021. [Causal Inference in Natural Language Processing: Estimation, Prediction, Interpretation and Beyond](http://arxiv.org/abs/2109.00725). arXiv: 2109.00725. [[中文阅读笔记]](https://github.com/badbadcode/Causality-NLP-Reading-List/blob/master/notes/Feder%20et%20al_2021_Causal%20Inference%20in%20Natural%20Language%20Processing%20-%20Estimation%2C%20Prediction%2C%20Beyond.md)
2. Katherine Keith, David Jensen, and Brendan O’Connor. 2020. Text and Causal Inference: A Review of Using Text to Remove Confounding from Causal Estimates. In *Proceedings of the 58th Annual Meeting of the Association for Computational Linguistics*, pages 5332–5344.

## 1. Robustness
### 1.1 Model Perspective

#### (1) Backdoor Adjustment
1. Shengyu Zhang, Tan Jiang, Tan Wang, Kun Kuang, Zhou Zhao, Jianke Zhu, Jin Yu, Hongxia Yang, and Fei Wu. 2021. [DeVLBert: Out-of-Distribution Visio-Linguistic Pretraining With Causality](https://openaccess.thecvf.com/content/CVPR2021W/CiV/html/Zhang_DeVLBert_Out-of-Distribution_Visio-Linguistic_Pretraining_With_Causality_CVPRW_2021_paper.html). pages 1744–1747. [[code]](https://github.com/shengyuzhang/DeVLBert)
2. Virgile Landeiro and Aron Culotta. 2016. [Robust Text Classification in the Presence of Confounding Bias](https://www.aaai.org/ocs/index.php/AAAI/AAAI16/paper/view/12445/11582). In *Thirtieth AAAI Conference on Artificial Intelligence*.
3. Virgile Landeiro and Aron Culotta. 2018. [Robust Text Classification under Confounding Shift](https://www.jair.org/index.php/jair/article/view/11248/26445). *Journal of Artificial Intelligence Research*, 63:391–419. [[code]](https://github.com/tapilab/jair-2018-confound),[[中文阅读笔记]](https://github.com/badbad[code]/Causality-NLP-Reading-List/blob/master/notes/Landeiro_Culotta_2018_Robust%20Text%20Classification%20under%20Confounding%20Shift.md)
4. Wenkai Zhang, Hongyu Lin, Xianpei Han, and Le Sun. 2021. [De-biasing Distantly Supervised Named Entity Recognition via Causal Intervention](https://aclanthology.org/2021.acl-long.371). In *Proceedings of the 59th Annual Meeting of the Association for Computational Linguistics and the 11th International Joint Conference on Natural Language Processing (Volume 1: Long Papers)*, pages 4803–4813. Association for Computational Linguistics. [[code]](github.com/zwkatgithub/DSCAU)
5. Yiquan Wu, Kun Kuang, Yating Zhang, Xiaozhong Liu, Changlong Sun, Jun Xiao, Yueting Zhuang, Luo Si, and Fei Wu. 2020. [De-Biased Court’s View Generation with Causality](https://aclanthology.org/2020.emnlp-main.56). In *Proceedings of the 2020 Conference on Empirical Methods in Natural Language Processing (EMNLP)*, pages 763–780. Association for Computational Linguistics. [[code]](https://aclanthology.org/2020.emnlp-main.56)
6. Zhen Bi, Ningyu Zhang, Ganqiang Ye, Haiyang Yu, Xi Chen, and Huajun Chen. 2021. [Interventional Aspect-Based Sentiment Analysis](http://arxiv.org/abs/2104.11681). *arXiv:2104.11681 [cs]*. [[code]](https://github.com/zjunlp/SENTA)
7. Virgile Landeiro and Aron Culotta. [Reducing confounding bias in observational studies that use text classiﬁcation](http://www.cs.iit.edu/~culotta/pubs/landeiro16reducing.pdf).

#### (2) Reweighting

1. Zheyan Shen, Peng Cui, Kun Kuang, Bo Li, and Peixuan Chen. 2018. Causally Regularized Learning with Agnostic Data Selection Bias. In *Proceedings of the 26th ACM international conference on Multimedia*, pages 411–419. Association for Computing Machinery. [[code]](https://github.com/Silver-Shen/Causally-Regularized-Learning),[[中文阅读笔记]](https://github.com/badbadcode/Causality-NLP-Reading-List/blob/master/notes/Shen%20et%20al_2018_Causally%20Regularized%20Learning%20with%20Agnostic%20Data%20Selection%20Bias.md)

### 1.2 Data Perspective

#### (1) Counterfactual Sample Generation

##### rule

1. Rowan Hall Maudslay, Hila Gonen, Ryan Cotterell, and Simone Teufel. 2019. [It’s All in the Name: Mitigating Gender Bias with Name-Based Counterfactual Data Substitution](https://www.aclweb.org/anthology/D19-1530). In *Proceedings of the 2019 Conference on Empirical Methods in Natural Language Processing and the 9th International Joint Conference on Natural Language Processing (EMNLP-IJCNLP)*, pages 5267–5275. Association for Computational Linguistics. 
2. Seungtaek Choi, Haeju Park, Jinyoung Yeo, and Seung-won Hwang. 2020. [Less is More: Attention Supervision with Counterfactuals for Text Classification](https://www.aclweb.org/anthology/2020.emnlp-main.543). In *Proceedings of the 2020 Conference on Empirical Methods in Natural Language Processing (EMNLP)*, pages 6695–6704. Association for Computational Linguistics.
3. Po-Sen Huang, Huan Zhang, Ray Jiang, Robert Stanforth, Johannes Welbl, Jack Rae, Vishal Maini, Dani Yogatama, and Pushmeet Kohli. 2020. [Reducing Sentiment Bias in Language Models via Counterfactual Evaluation](https://www.aclweb.org/anthology/2020.findings-emnlp.7). In *Findings of the Association for Computational Linguistics: EMNLP 2020*, pages 65–83. Association for Computational Linguistics. 

##### propensity score matching 

1. Zhao Wang and Aron Culotta. 2021. [Robustness to Spurious Correlations in Text Classification via Automatically Generated Counterfactuals](https://ojs.aaai.org/index.php/AAAI/article/view/17651). *Proceedings of the AAAI Conference on Artificial Intelligence*, 35(16):14024–14031. [[code]](https://github.com/tapilab/aaai-2021-counterfactuals), [[中文阅读笔记]](https://github.com/badbad[code]/Causality-NLP-Reading-List/edit/master/notes/Wang_Culotta_2020_Robustness%20to%20Spurious%20Correlations%20in%20Text%20Classification%20via%20Automatically.md)

##### human in loop

1. Divyansh Kaushik, Eduard Hovy, and Zachary Lipton. 2019. [Learning The Difference That Makes A Difference With Counterfactually-Augmented Data](https://arxiv.org/pdf/1909.12434.pdf). [[code]](https://github.com/acmi-lab/counterfactually-augmented-data)

##### language model

1. Tongshuang Wu, Marco Tulio Ribeiro, Jeffrey Heer, and Daniel S. Weld. 2021. [Polyjuice: Generating Counterfactuals for Explaining, Evaluating](https://arxiv.org/pdf/2101.00288.pdf), and Improving Models. *arXiv:2101.00288 [cs]*. [[code]](https://github.com/tongshuangwu/polyjuice)
2. Nishtha Madaan, Inkit Padhi, Naveen Panwar, and Diptikalyan Saha. 2021. [Generate Your Counterfactuals: Towards Controlled Counterfactual Generation for Text](https://ojs.aaai.org/index.php/AAAI/article/view/17594). In *Proceedings of the AAAI Conference on Artificial Intelligence*, volume 35, pages 13516–13524. [[code]](https://github.com/annon-author9/GYC)
3. Linyi Yang, Jiazheng Li, Padraig Cunningham, Yue Zhang, Barry Smyth, and Ruihai Dong. 2021. [Exploring the Efficacy of Automatically Generated Counterfactuals for Sentiment Analysis.](https://aclanthology.org/2021.acl-long.26.pdf) In Proceedings of the 59th Annual Meeting of the Association for Computational Linguistics and the 11th International Joint Conference on Natural Language Processing (Volume 1: Long Papers), pages 306–316. Association for Computational Linguistics. [[code]](https://github.com/lijiazheng99/Counterfactuals-for-Sentiment-Analysis)

## Fairness 



## Interpretability
### Causal Feature Identification for NLP
1. Michael J. Paul. 2017. [Feature Selection as Causal Inference: Experiments with Text Classification](https://aclanthology.org/K17-1018.pdf). In *Proceedings of the 21st Conference on Computational Natural Language      Learning (CoNLL 2017)*, pages 163–172. Association for Computational Linguistics. [[code]](https://github.com/tapilab/jair-2018-confound)
2. Zhao Wang and Aron Culotta. 2020. [Identifying Spurious Correlations for Robust Text Classification](https://aclanthology.org/2020.findings-emnlp.308.pdf). In *Findings of the Association for Computational Linguistics: EMNLP 2020*, pages 3431–3440. Association for Computational Linguistics. [[code]](https://github.com/tapilab/emnlp-2020-spurious)

### Causal Model Explanation
1. Amir Feder, Nadav Oved, Uri Shalit, and Roi Reichart. 2021. [CausaLM: Causal Model Explanation Through Counterfactual Language Models](https://direct.mit.edu/coli/article/doi/10.1162/coli_a_00404/98518/CausaLM-Causal-Model-Explanation-Through). *Computational Linguistics*:1–54. [[code]](https://github.com/amirfeder/CausaLM)

