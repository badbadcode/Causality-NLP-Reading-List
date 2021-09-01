## 动机

来自[计算社会科学领域](https://www.zhihu.com/question/51735457)

> 2009年，Lazer等人发表《计算社会科学》，第一次正式提出了计算社会科学的概念，概括了计算社会科学的出现及其发展，强调了网络科学研究在其中所扮演的角色和数字化媒体所提供的机遇，标志着计算社会科学的诞生。从那时以来，有关计算社会科学的研究得到了学术界广泛关注，并且产生了大量的研究成果。

x代表社交用户的写作文本，y代表用户所属类别。====> 比如：通过博文预测精神状况；通过评论预测用户性格；在这样的设置中，研究者对于特定的混杂变量有先验知识。比如性别 $Z$​ 对发文用词​ $X$ 以及 精神状态 $Y$ 同时相关。

There are many reasons why $P_{train}(Y |Z)$​ may not equal  $P_{train}(Y |Z)$​​ 

- 数据来自不同的时间
- bad luck ,小样本的数据集中的关系在更大人口上不成立

我们的目标是：**构建对 confound shifts 鲁棒的文本分类器。**

## 方法

 我们将后门调整（aka covariate adjustment or statistical adjustment）思路引入分类器：在训练的时候以混杂变量为条件，在测试的时候汇总。

强调：我们的方法启发于因果推断技巧，但我们的目标是稳健文本分类，而不是因果推断。

> Indeed, it would be strange to assert that using a term causes one to have a class label.

我们在5个文本分类任务上进行试验评估，分别设置了两组实验：

1. 我们在这组实验中，注入混杂变差（通过对训练集和测试集二次采样），观察在不同程度的shift下，不同的方法表现。
2. 考虑自然设置，即数据来源于不同的时间。

我们发现所提方案在多组数据集上都优于baselines. 当confounding shift 非常高，我们的方法提升最多20%的准确率。我们仍然观察到我们的方法的有限性，在有些设置下，会降低准确率，我们讨论了解决这些问题可能的方向。

## 相关工作

- Selection bias in text classification occurs when the distribution of text features changes from training to testing  $P_{train}(X) \neq P_{test}(X)$​​​  

- 数据不平衡：$P_{train}(Y) \neq P_{test}(Y)$​

- “fairness” in machine learning

  确保分类器的预测在涉及人口属性的时候，是一致的。

  

## 具体方法

### 后门调整

方法bone来自作者上一篇工作 (Landeiro and Culotta, 2016), 
$$
L(D, \theta)=\sum_{i \in D} \log p_{\theta}\left(y_{i} \mid \mathbf{x}_{i}, z_{i}\right)-\lambda_{x} \sum_{k}\left(\theta_{k}^{x}\right)^{2}-\lambda_{z} \sum_{k}\left(\theta_{k}^{z}\right)^{2}
$$

> 在训练的时候，学习怎么预测条件概率，通过惩罚项，以及增大混杂的变量值，增加模型对于混杂的注意（只有两个特征，而X有很多特征），采样控制confound shift的强度，并满足以下条件。


$$
\begin{aligned}
&P_{\text {train }}(y=1 \mid z=1)=b_{\text {train }} \\
&P_{\text {test }}(y=1 \mid z=1)=b_{\text {test }} \\
&P_{\text {train }}(Y)=P_{\text {test }}(Y) \\
&P_{\text {train }}(Z)=P_{\text {test }}(Z)
\end{aligned}
$$

在3个文本分类的实验中证明所提方案的鲁棒性，根据推特的文本预测地理位置，性别是混杂；根据电影评论预测情感，电影类别是混杂。还有个政治相关的实验。

本文的方法在上述工作的基础上作了以下改进：

1. 除了人工赋予shift，考虑使用时间流动的实验数据；
2. 超参选择
3. 同时存在多个混杂变量

**At training time**, we use the labeled data to:

- fit a logistic regression model to  $p(y|\overrightarrow{x},z)$​​

-  compute $p(z)$​ using 
  $$
  p(z=k)=\frac{\sum_{i \in D} \mathbf{1}\left[z_{i}=k\right]}{|D|}
  $$

**At prediction time**, for each instance ~x in the testing set:

- we compute   $p(y|\overrightarrow{x},z)$​ for all possible values of $z$ ​using the logistic regression model
  fit at training time;
- we use $p(z)$ computed at training time and $p(y \mid x)=\sum_{z \in Z} p(y \mid x, z) p(z)$ to compute  $p(y|\overrightarrow{x})$​



## Reference

1. Virgile Landeiro and Aron Culotta. 2016. Robust Text Classification in the Presence of Confounding Bias. 





