# SVM
learning report about SVM
支持向量机
SVM
SVM - Support Vector Machine：支持向量机，其含义是通过支持向量运算的分类器。其中“机”的意思是机器，可以理解为分类器。在求解的过程中，会发现只根据部分数据就可以确定分类器，这些数据称为支持向量。
见下图，在一个二维环境中，其中点R，S，G点和其它靠近中间黑线的点可以看作为支持向量，它们可以决定分类器，也就是黑线的具体参数。
   ![image](https://github.com/fuxiyu399/SVM/blob/master/a.png)
线性分类：
在训练数据中，每个数据都有n个的属性和一个二类类别标志，我们可以认为这些数据在一个n维空间里。我们的目标是找到一个n-1维的超平面（hyperplane），这个超平面可以将数据分成两部分，每部分数据都属于同一个类别。
其实这样的超平面有很多，我们要找到一个最佳的。因此，增加一个约束条件：这个超平面到每边最近数据点的距离是最大的。也成为最大间隔超平面（maximum-margin hyperplane）。这个分类器也成为最大间隔分类器（maximum-margin classifier）。
支持向量机是一个二类分类器。
f(x) = xw^T + b
w 和 b 是训练数据后产生的值。
KTT条件
 ！[iamge](https://github.com/fuxiyu399/SVM/blob/master/b.png)
 ![image](https://github.com/fuxiyu399/SVM/blob/master/c.png)
 ![image](https://github.com/fuxiyu399/SVM/blob/master/d.png)
 
核心思想：
SVM的目的是要找到一个线性分类的最佳超平面 f(x)=xwT+b=0。求 w 和 b。
首先通过两个分类的最近点，找到f(x)的约束条件。
有了约束条件，就可以通过拉格朗日乘子法和KKT条件来求解，这时，问题变成了求拉格朗日乘子ai 和 b。
对于异常点的情况，加入松弛变量ξ来处理。
使用SMO来求拉格朗日乘子ai和b。这时，我们会发现有些ai=0，这些点就可以不用在分类器中考虑了。
惊喜! 不用求w了，可以使用拉格朗日乘子ai和b作为分类器的参数。
非线性分类的问题：映射到高维度、使用核函数。
SMO算法优化：
核心公式：
![image](https://github.com/fuxiyu399/SVM/blob/master/20171004151936130.png)
 ![image](https://github.com/fuxiyu399/SVM/blob/master/e.png)
 
优化方法：
最外层循环，首先在样本中选择违反KKT条件的一个乘子作为最外层循环，然后用”启发式选择”选择另外一个乘子并进行这两个乘子的优化
在非边界乘子中寻找使得|E_i - E_j|最大的样本
如果没有找到，则从整个样本中随机选择一个样本
完整版SMO算法：
完整版Platt SMO算法是通过一个外循环来选择违反KKT条件的一个乘子，并且其选择过程会在这两种方式之间进行交替：
在所有数据集上进行单遍扫描
在非边界α中实现单遍扫描
非边界α指的就是那些不等于边界0或C的α值，并且跳过那些已知的不会改变的α值。所以我们要先建立这些α的列表，用于才能出α的更新状态。
在选择第一个α值后，算法会通过“启发选择方式”选择第二个α值。
完整版SMO算法和简化版算法对比:
  ![image](https://github.com/fuxiyu399/SVM/blob/master/f.png)
  ![image](https://github.com/fuxiyu399/SVM/blob/master/g.png)
图中画红圈的样本点为支持向量上的点，是满足算法的一种解。完整版SMO算法覆盖整个数据集进行计算，而简化版SMO算法是随机选择的。可以看出，完整版SMO算法选出的支持向量样点更多，更接近理想的分隔超平面。
非线性SVM：
核函数;
对于线性可分的平面其抄平面方程：
 ![image](https://github.com/fuxiyu399/SVM/blob/master/h.png)
对于线性不可分：
 ![image](https://github.com/fuxiyu399/SVM/blob/master/j.png)

