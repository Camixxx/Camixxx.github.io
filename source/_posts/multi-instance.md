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
而这篇paper受深度神经网络和多实例学习的方法所启发,把多实例学习转换为多实例的标签任务,来提高INbrest乳腺X光数据集上的分类和检测的鲁棒性.


<!--more-->


### 概念与相关工作

多实例学习,可以看做是面向多个实例, 而非单个实例的监督学习. 以二分类为例, 将多个实例看做一组, 若其中有一个实例为阳性, 则整组可标记为阳性; 而只有在组内所有实例为阴性时, 该组的标记才是阴性. 而且许多医学图像数据都涉及到一个病人的病例下包含多个图像的情况.

标准MI假设, 是Dietterich et al. (1997) and Maron & Lozano-P´erez (1997)论文中提出的关于多实例的假设. 每个实例  x ∈ X {\displaystyle x\in {\mathcal {X}}} x\in {\mathcal {X}} 

1. 多实例学习在机器学习中的研究
	
    [SVM Multi-instance[1]](#ref1) , [Marginalized kernel[2]](#ref2), [Multi-class classification[3]](#ref2)
    

2. 多实例学习与神经网络的结合 

	[多实例图像分类与自动标注[4]](#ref4)

在这篇文章中


### 引用 

1. <a id="ref1" href="https://www.researchgate.net/publication/2838430_Multiple_Instance_Learning_with_Generalized_Support_Vector_Machines">Andrews S, Hofmann T, Tsochantaridis I. Multiple instance learning with generalized support vector machines[C] Eighteenth national conference on Artificial intelligence. American Association for Artificial Intelligence, 2002:943-944.</a>

2. <a id="ref2" href="https://dl.acm.org/citation.cfm?id=1625421">Kwok J T, Cheung P M. Marginalized multi-instance kernels[C] International Joint Conference on Artifical Intelligence. Morgan Kaufmann Publishers Inc. 2007:901-906.</a>


3. <a id="ref3" href="https://arxiv.org/pdf/0808.3231.pdf">Zhou Z H, Zhang M L, Huang S J, et al. Multi-Instance Multi-Label Learning[J]. Artificial Intelligence, 2008, 176(1):2291-2320.</a>
<!-- (h) -->

4. <a id="ref4" href="https://ieeexplore.ieee.org/document/7298968/">Wu J, Yu Y, Huang C, et al. Deep multiple instance learning for image classification and auto-annotation[C]// Computer Vision and Pattern Recognition. IEEE, 2015:3460-3469.</a>


5. <a id="ref5" href>Zhou Z H, Zhang M L, Huang S J, et al. Multi-Instance Multi-Label Learning[J]. Artificial Intelligence, 2008, 176(1):2291-2320.</a>

6. <a id="ref6" href>Zhou Z H, Zhang M L, Huang S J, et al. Multi-Instance Multi-Label Learning[J]. Artificial Intelligence, 2008, 176(1):2291-2320.</a>