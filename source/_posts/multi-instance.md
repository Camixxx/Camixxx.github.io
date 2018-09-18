---
title: Deep Multi-instance Networks with Sparse Label Assignment
categories:
- DL
- paper
tags:
- DL
- Neural Network
- Medical AI
mathjax: true
date: 2018-09-17 15:30:01
---

最近读了这篇paper: 

    Deep Multi-instance Networks with Sparse Label Assignment for Whole Mammogram Classification(Wentao Zhu, Qi Lou, Yeeleng Scott Vang, and Xiaohui Xie)

因为手上的数据标签非常粗糙,质量低下,所以想要借鉴一下在医学图像数据里面的处理方法.之后还会整理关于弱监督的一些文章.

文中提到医学数据的学习和训练存在的问题, 由于问题是数据驱动的, 而整个数据依赖于经验丰富的专家或者病理结果等的金标准,所以数据的处理和获得都需要耗费人力物力.
而这篇paper受深度神经网络和多实例学习的方法所启发,利用多实例学习与深度神经网络的结合来提高INbrest乳腺X光数据集上的分类和检测的鲁棒性.


<!--more-->


### 概念与相关工作

多实例学习(MIL),可以看做是面向多个实例, 而非单个实例的监督学习. 以二分类为例, 将多个实例看做一个包, 若其中有一个实例为阳性, 则整组可标记为阳性; 而只有在组内所有实例为阴性时, 该组的标记才是阴性. 

标准MI假设, 是Dietterich(1997) 和 Maron & Lozano-P´erez(1997) 论文中提出的关于多实例的假设. 每个实例 x ∈ X 与标签 y ∈ {0, 1}之间存在隐藏的联系,可以通过学习得到. 则这一组(x, y) 被称作"实例级概念". 而在多个实例级概念的集合中,  B = {(x1, y1), …, (xn, yn)} 是一个包, 包中如果有一个阳性实例, B为阳性, 所有实例为阴性时, B的标签为阴性. 因此整个假设是不对称的, 当正负样本调转的时候假设含义则完全不同了.

1. 多实例学习在机器学习中的研究
	
    [SVM Multi-instance[1]](#ref1) , [Marginalized kernel[2]](#ref2), [Multi-class classification[3]](#ref2)
    

2. 多实例学习与神经网络的结合 

	[多实例图像分类与自动标注[4]](#ref4)

    这篇文章基于多实例学习的假设提出了一个弱监督学习框架来完成图像的分类和标注任务, 对没有标签或者标签嘈杂的大数据来说,可以把得到的每个关键词标记看做一个实例,而一张图像拥有多个关键词,可看做一个包.
    在一般的多实例训练的时候,实例级别的标签可以说是未知的,仅有包级标签参与训练,则这样的训练方法可以得到较高的召回率.

    提出的DMIL结构如下:

    ![DMIL](multi-1.png)

    Deep-MIL是对这一组DNN网络最后的值取Max.将网络收集到的嘈杂关键词作为输入,来进行图像真正关键词的预测.
    而Joint Deep-MIL是结合CNN(图像输入)和DNN(关键词输入)来同时学习图像和关键词之间关系.

    其他还有 [多实例局部识别[5]](#ref5)等相关的研究.


### 方法

而许多医学图像数据都涉及到一个病人的病例下包含多个图像的情况, 因而此处的实例指的是单张乳腺图片, 最后得到的输出为乳腺X光图像分类的良恶性结果.

1. Max Pooling: 使用最大池化计算, 只从排序层中提取最大的元素
 
p(y = 1|I, θ) = max{r1, r2, ..., rm },

根据多实例假设, 最后网络输出时需要取最大的结果, 而如果将其进行排序, 则可认为排在前列的实例与恶性病灶相关性更大, 排在首位的则是最后的输出. 因此:

${
L\_{maxpooling} = 
}$


L maxpooling = −
N
X
log(p(y n |I n , θ)) +
n=1
λ
kθk 2

2. Label assignment-based MIL: 基于标签分配的多实例学习以利用所有的元素




3. Sparse multi-instance learning: 稀疏多示例学习以增加稀疏约束, 最后一点的效果最好.






### 引用 

1. <a id="ref1" href="https://www.researchgate.net/publication/2838430_Multiple_Instance_Learning_with_Generalized_Support_Vector_Machines">Andrews S, Hofmann T, Tsochantaridis I. Multiple instance learning with generalized support vector machines[C] Eighteenth national conference on Artificial intelligence. American Association for Artificial Intelligence, 2002:943-944.</a>

2. <a id="ref2" href="https://dl.acm.org/citation.cfm?id=1625421">Kwok J T, Cheung P M. Marginalized multi-instance kernels[C] International Joint Conference on Artifical Intelligence. Morgan Kaufmann Publishers Inc. 2007:901-906.</a>


3. <a id="ref3" href="https://arxiv.org/pdf/0808.3231.pdf">Zhou Z H, Zhang M L, Huang S J, et al. Multi-Instance Multi-Label Learning[J]. Artificial Intelligence, 2008, 176(1):2291-2320.</a>
<!-- (h) -->

4. <a id="ref4" href="https://ieeexplore.ieee.org/document/7298968/">Wu J, Yu Y, Huang C, et al. Deep multiple instance learning for image classification and auto-annotation[C]// Computer Vision and Pattern Recognition. IEEE, 2015:3460-3469.</a>


5. <a id="ref5" href="https://www.researchgate.net/publication/293012616_Multi-Instance_Deep_Learning_Discover_Discriminative_Local_Anatomies_for_Bodypart_Recognition">Yan Z, Zhan Y, Peng Z, et al. Multi-instance Deep Learning: Discover Discriminative Local Anatomies for Bodypart Recognition.[J]. IEEE Transactions on Medical Imaging, 2016, 35(5):1332-1343.</a>

6. <a id="ref6" href>Zhou Z H, Zhang M L, Huang S J, et al. Multi-Instance Multi-Label Learning[J]. Artificial Intelligence, 2008, 176(1):2291-2320.</a>


6. <a id="ref6" href>Zhou Z H, Zhang M L, Huang S J, et al. Multi-Instance Multi-Label Learning[J]. Artificial Intelligence, 2008, 176(1):2291-2320.</a>


6. <a id="ref6" href>Zhou Z H, Zhang M L, Huang S J, et al. Multi-Instance Multi-Label Learning[J]. Artificial Intelligence, 2008, 176(1):2291-2320.</a>


