# Causally Regularized Learning with Agnostic Data Selection Bias （Shen, MM18）

## Background

### OOD Problem:

$$
P_{tr}(X,Y) \ne P_{te}(X,Y)
$$

<img src="https://gitee.com/hanmingyue/picgo/raw/master/pic/image-20211201202032545.png" alt="image-20211201202032545" style="zoom: 80%;" align=center/>

i.e.
$$
P_{tr}(Y|X)* P_{tr}(X)\ne P_{te}(Y|X)* P_{te}(X)
$$

- $$ P_{tr}(Y|X)= P_{te}(Y|X), P_{tr}(X) \ne P_{te}(X)$$​

  [covariate shift problem](https://blog.csdn.net/gzmfxy/article/details/78905042)，这种OOD情况比较普遍，仅仅是X 的分布有变化，条件概率分布不变，[Shen et al., 2021](http://arxiv.org/abs/2108.13624) 在综述中这么定义。The marginal distribution of $X$​​ shifts from training phase to test phase while the label generation mechanism keeps unchanged.

  **adaptation:** 目标领域的unlabeled数据 $X$ 已知

  **generalization:** 对于目标领域一无所知

- $$ P_{tr}(Y|X)\ne P_{te}(Y|X), P_{tr}(X) \ne P_{te}(X)$$​

  $$ P_{tr}(Y|X)\ne P_{te}(Y|X), P_{tr}(X) = P_{te}(X)$$​

  concept shift problem, 综述（[Gama et.al, 2014](https://dl.acm.org/doi/pdf/10.1145/2523813)）

### A New Problem in OOD setting

- Domain adaptation

  Prior knowledge of unlabeled data in target domain

- Domain generalization

  explicit domain separation of training data

- Agnostic data selection bias
  More general and realistic

 It is well recognized that causal variables are stable across different domains or data selection bias, due to the **rigorous scrutiny on confounding effects in identifying causal variables**.

The stability of causal variables is mainly reflected by the fact that **the conditional distribution of outcome variable given those causal variables remains invariant across different domains**. 

### Retrospect on CI

identifying causal effect of **a** variable:

- randomized experiments like A/B testing 
  - gold standard 
  - Infeasible, expensive
-  Estimate causal effect directly from observational data
  - Matching-based method
  - Propensity  Score based method
    - Weighting
    - Doubly Robust
    - Data-Driven Variable Decomposition
  - Directly Confounder Balancing
    - Entropy Balancing
    - Approximate Residual Balancing
    - Differentiated Confounder Balancing

特别地，我在这个文档里介绍了对 **加权使得变量之间独立** 的直观理解。

## CRLR Method

基于causal regularizer和logistic regression学习一个加权的logistic regression，得到的系数从某种意义上可以被称为因果系数，基于这样的系数给出的预测结果具备可解释性和稳定性。当然可以将此处的LR换成深度模型。

1个变量为处置变量时，样本权重的loss：

<img src="https://gitee.com/hanmingyue/picgo/raw/master/pic/image-20211128221051432.png" alt="image-20211128221051432" style="zoom: 33%;" />

多个变量为处置变量时，依次将每个变量都作为T，计算其平衡损失，并加总，公式如下：<img src="https://gitee.com/hanmingyue/picgo/raw/master/pic/image-20211128221211461.png" alt="image-20211128221211461" style="zoom: 67%;" />

针对每一个处置变量，平衡混杂的损失函数计算方式：

​                 ![image-20211128230441084](../../../AppData/Roaming/Typora/typora-user-images/image-20211128230441084.png)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        

整体的优化问题是：

<img src="https://gitee.com/hanmingyue/picgo/raw/master/pic/image-20211128231224469.png" alt="image-20211128231224469" style="zoom: 80%;" />

转换成：

<img src="https://gitee.com/hanmingyue/picgo/raw/master/pic/image-20211128231258530.png" alt="image-20211128231258530" style="zoom:80%;float:center" />

很难有解析解，我们使用迭代的方式求解，参考DCB（KDD2017）的算法，使用proximal gradient algorithm依次对两个参数求解。



## Experiments

### **Experiments on Synthetic Dataset** 

<img src="https://gitee.com/hanmingyue/picgo/raw/master/pic/image-20211201233335902.png" alt="image-20211201233335902" style="zoom:80%;" />

Logistic Regression present drastic fluctuation (larger standard error) over different bias rate on testing set across different training settings, while CRLR achieve a relative more stable and accurate prediction result

### **Experiments on YFCC100M Dataset** 

#### Robustness

<img src="https://gitee.com/hanmingyue/picgo/raw/master/pic/image-20211201233440948.png" alt="image-20211201233440948" style="zoom:80%;" />

- 10 categories
  - 5 contexts. For each category, we use context 1,2,3 for training, context 4 for validation and context 5 for testing 
- Compare with LR
  - confounder balancing term and its seamless joint with logistic regression model
- Compare with two-step
  - the importance of jointly optimizing causal feature selection and classification

#### When bias is more serious 

![image-20211201233626209](https://gitee.com/hanmingyue/picgo/raw/master/pic/image-20211201233626209.png)

- quantify the  bias level of a category with the EMD distance between the average feature vector of training images and the average feature vector of testing images
- relative F1 improvement and the category bias level are correlated to some degree

#### Make the predictive models more explainable

![image-20211201233800531](https://gitee.com/hanmingyue/picgo/raw/master/pic/image-20211201233800531.png)

- CRLR are positioned on the major object

- LR are positioned on context features

### **Experiments on Office-Caltech Dataset** 

when there is no explicit distribution or domain shift

- images from four distinct domains

  - Amazon, DSLR, Webcam, and Caltech
  - 1000 images on average

- domain adaptation

  - data collecting process 

  <img src="https://gitee.com/hanmingyue/picgo/raw/master/pic/image-20211201233927324.png" alt="image-20211201233927324" style="zoom:80%;" />

the advantage of CRLR is more obvious when we have less training samples in the source domain. 

### **Experiments on WeChat Ads Dataset**

<img src="https://gitee.com/hanmingyue/picgo/raw/master/pic/image-20211201234007018.png" alt="image-20211201234007018" style="zoom:80%;" />

- in the group Aдe ∈ [20, 30) where no selection bias exists, i.i.d. setting
  - CRLR algorithm is comparable to baselines
- tested on other three groups
  - CRLR consistently outperforms the other baselines and obtains the smallest error
     regression coefficients in CRLR imply causations which are more stable and insensitive to distribution shift induced by selection bias
- unsatisfactory performance of two-step method
  - The importance of jointly optimizing causal inference and predictive modeling

## My Questions

1. 选择偏差与confounder均是CI领域中相关不等于因果的重要来源，二者有何共同的地方？为什么这篇论文前面是在讲选择偏差的问题，后面的解决方案是针对confounder balancing? 选择偏差造成混淆，造成内生性？

2. 将所有变量作为confounder ，这样的问题是，会不会打开对撞路径。这篇文章不必考虑？还是说学习权重$\beta$ 的时候，对撞因子会自动学习到 0 的系数？但是针对不同的处置变量，其他变量是否为对撞因子是不一定的。也就是说不可能一个$\beta$ 就能搞定。









