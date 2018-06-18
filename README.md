# imbalanced_classification
处理机器学习中不平衡数据集

最近在做一个分类项目，包含有17类，数据集大小为5千左右，并且每个类别的样本数量相差很大，多的占据了总数据集一半，少的一二十条。刚开始拿到这批数据，想过用一些方法造数据，但是觉得代价也大，周期太长，造的质量也不能保证。于是调研了一些方法，做出了一个baseline版本。
以下是针对不平衡数据集问题的调研总结：
 
1，https://www.analyticsvidhya.com/blog/2017/03/imbalanced-classification-problem/ 介绍了几种数据采样机制（使得类别之间的数据数量平衡，里面提到一个基于聚类的过采样，想到k的选择，就没试过这个方法）、模型的选择（从模型层面考虑哪种算法更适合不平衡数据集问题），最后提到了不要用准确率来衡量分类器性能，而要用混淆矩阵、roc曲线等
（对应的中文翻译：https://mp.weixin.qq.com/s?__biz=MzA3MzI4MjgzMw==&mid=2650724464&idx=1&sn=1f34358862bacfb4c7ea17c864d8c44d）
2，https://machinelearningmastery.com/tactics-to-combat-imbalanced-classes-in-your-machine-learning-dataset/ 针对不平衡数据集问题介绍了八种策略，从评价分类器性能的指标选择（初次接触到Kappa：https://en.wikipedia.org/wiki/Cohen%27s_kappa）到数据采样技术，再到Spot-Checking Algorithms等，作者的意见比较中肯，其他相关的文章质量也高，例如：https://machinelearningmastery.com/why-you-should-be-spot-checking-algorithms-on-your-machine-learning-problems/
3，http://www.quora.com/In-classification-how-do-you-handle-an-unbalanced-training-set 对不平衡问题的一些解决方法，觉得脑洞很大
4，https://datascience.stackexchange.com/questions/27671/how-do-you-apply-smote-on-text-classification 利用smote造文本语料
5，http://www.algorithmdog.com/unbalance 也是对数据的采样机制介绍，但里面提到复制样本数量不能改变svm的支持向量，这点没理解，按理说损失值变了
6，https://blog.csdn.net/a358463121/article/details/52304670 数据采样机制的详细介绍
7，Exploratory undersampling for class-imbalance learning  
    具体原理：1)从多数类中有放回的随机采样n次，每次选取与少数类数目相近的样本个数，那么可以得到n个样本集合记作。

            2)然后，将每一个多数类样本的子集与少数类样本合并并训练出一个模型，可以得到n个模型。

            3)最终将这些模型组合形成一个集成学习系统，最终的模型结果是这n个模型的平均值。

8,imblearn python对应的数据采样库

总结：不要只实验自己熟悉的算法。
     对比实验的严谨性很重要，最好是整理一套算法工具箱，例如基于实例的knn、基于核函数的svm、基于规则的决策树。
     
     
最后我用的baseline用的是smote + boosting算法
     
