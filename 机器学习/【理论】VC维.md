# VC维
vc维是衡量机器学习算法优劣和过拟合程度的一种理论.
看到一篇博客在介绍[VC维的来龙去脉](http://www.flickering.cn/machine_learning/2015/04/vc%E7%BB%B4%E7%9A%84%E6%9D%A5%E9%BE%99%E5%8E%BB%E8%84%89/),形式化而详细地讲解了VC维的诞生和意义.我便把自己的理解写下:
## Hoeffding不等式
不论是分类还是回归,都在处理抽样数据,通过样本训练出模型,并应用到总体上.也就是train和test过程.涉及到总体和样本就自然会引出一个问题:样本的统计特征是否能准确反映出总体的统计特征?有多准确呢?

![bin_sample](https://github.com/StriderStranger/GeistDenkmal/blob/master/%E6%9C%BA%E5%99%A8%E5%AD%A6%E4%B9%A0/res/bin_sample.png)

Hoeffding不等式在一定程度上回答了这个问题.Hoeffding不等式是关于一组随机变量均值的概率不等式.

![hoeffding](https://github.com/StriderStranger/GeistDenkmal/blob/master/%E6%9C%BA%E5%99%A8%E5%AD%A6%E4%B9%A0/res/hoeffding.png)

从hoeffding不等式可以看出，当N逐渐变大时，不等式的UpperBound越来越接近0，所以样本期望越来越接近总体期望!

一个基本的机器学习过程表示:通过算法A,在假设空间H中,根据样本集D,选择最好的假设h,使得h尽可能近似于理想模型f.

**Eout(h)**,为理想情况下,总体的损失的期望,称作expected loss.

**Ein(h)**,为训练样本上损失的期望,称作expirical loss.
当训练样本N足够大,且样本独立同分布时,可以通过样本集的Ein(h)推测总体的Eout(h),基于Hoeffding不等式有:

![Einout_hoeffding](https://github.com/StriderStranger/GeistDenkmal/blob/master/%E6%9C%BA%E5%99%A8%E5%AD%A6%E4%B9%A0/res/Einout_hoeffding.png)

该不等式只针对某一个特定的模型h(x),当H中有M个假设模型时,就有如下不等式:

![M_hoeffding](https://github.com/StriderStranger/GeistDenkmal/blob/master/%E6%9C%BA%E5%99%A8%E5%AD%A6%E4%B9%A0/res/M_hoeffding.png)

这就说明,模型对样本的损失与对总体的损失间的差距和样本数N,假设数M密切相关.

## 学习可行的两个核心条件
**什么情况下Learning是可行的?**
1. 如果假设空间H的size M是有限的,当N足够大时,那么对假设空间中任意一个h,Eout(h)约等于Ein(h);
2. 利用算法A从假设空间H中,挑选出一个h,使得Ein(h)接近于0,那么PAC而言,Eout(h)也接近于0;
## Effective Number
## Break Point & Shatter
## VC维