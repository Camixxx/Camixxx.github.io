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

---

最近读了这篇paper: Deep Multi-instance Networks with Sparse Label Assignment for Whole Mammogram Classification(Wentao Zhu, Qi Lou, Yeeleng Scott Vang, and Xiaohui Xie)

因为手上的数据标签非常粗糙,质量低下,所以想要借鉴一下在医学图像数据里面的处理方法.之后还会整理关于弱监督的一些文章.

文中提到医学数据的学习和训练存在的问题, 由于问题是数据驱动的, 而整个数据依赖于经验丰富的专家或者类似于病理结果这一类的金标准,所以数据的处理和获得都需要耗费人力物力.
而这篇paper受深度神经网络和多实例学习的方法所启发,把多实例学习转换为多实例的标签任务,来提高INbrest乳腺X光数据集上的分类和检测的鲁棒性.


<!--more-->


[TOC]

### 相关工作

1. 多实例学习在机器学习中的研究
	
    [SVM Multi-instance](https://www.researchgate.net/publication/2838430_Multiple_Instance_Learning_with_Generalized_Support_Vector_Machines)。
	
    Andrews S, Hofmann T, Tsochantaridis I. Multiple instance learning with generalized support vector machines[C]// Eighteenth national conference on Artificial intelligence. American Association for Artificial Intelligence, 2002:943-944.
	
    [Marginalized kernel](https://dl.acm.org/citation.cfm?id=1625421)。
    
    Kwok J T, Cheung P M. Marginalized multi-instance kernels[C]// International Joint Conference on Artifical Intelligence. Morgan Kaufmann Publishers Inc. 2007:901-906.
    
    [Multi-class classification](hhttps://arxiv.org/pdf/0808.3231.pdf)。
    
    Zhou Z H, Zhang M L, Huang S J, et al. Multi-Instance Multi-Label Learning[J]. Artificial Intelligence, 2008, 176(1):2291-2320.
    
2. 多实例学习与神经网络的结合 

	[多实例图像分类与自动标注](https://ieeexplore.ieee.org/document/7298968/)
    Wu J, Yu Y, Huang C, et al. Deep multiple instance learning for image classification and auto-annotation[C]// Computer Vision and Pattern Recognition. IEEE, 2015:3460-3469.
    
    
    
	