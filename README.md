# GNN-Embedding
## 初入GNN，特别是GCN，现在开始记录一些近期阅读的论文和一些感触，同时也为了避免过多的重复阅读，希望广大同学一起交流。对GCN的理解十分浅显，目前只是了解了一部分的拉普拉斯变换，傅里叶变换以便于在傅里叶域上做卷积操作。在图上做卷积首先和在image等regular structure上本质区别在于其空间性，图片每一个pixel周围的pixel位置固定，而图上的话得考虑其邻居，是一个立体结构。目前理解是图上卷积因为每一次都从周围的邻居节点的向量中进行累加作为该节点的向量表示，那么在迭代下，最终收敛时每个节点应考虑到了整个图上的结构信息包括节点的属性，而非仅仅是自身相邻一阶或二阶的邻居属性，这是我理解的对整个图做操作的一种形式。

## 1. [convolutional networks on graphs for learning molecular fingerprints](http://papers.nips.cc/paper/5954-convolutional-networks-on-graphs-for-learning-molecular-fingerprints.pdf)
### 这篇文章主要是在分子结构上做一个操作，其中介绍了Circular fingerprints和differentiable fingerprints算法 第一个算法简单来说就是每一层对每一个节点周围的邻居包括其自身属性进行相加(类比卷积)，然后通过一个hash函数作为该节点的属性，并用mod操作映射到所谓的fingerprint向量上，而这个fingerprint每一个unit用来表示某种特殊的子结构(这样对于一个完全连接图来说，它只会映射到一个index上，保证了只有一个子结构)。最终整个molecule就可以用这些子结构的集合来表示(全局上pooling操作，将任意长度的Graph映射到fix长度的向量上)，其子结构的大小取决于网络的层数（也应取决于其节点个数）。 第二个算法是对上述算法中一些离散操作进行连续可导的泛化，用一层Neural Network来替代，并用sigmoid函数来保证其连续且平滑，而对于Index方法，由于每个节点均能决定fingerprint上一个bit上的值，那么对于小分子但是fingerprint的长度又很长时，势必有稀疏问题，也是用一个softmax来代替这个index即原始的mod操作，来类比每种category的概率，然后将这些概率pooling一下来表示原始的molecule 文中也提到了第一个算法不收到节点排序问题影响，解决办法是一对节点的属性向量进行一个映射到scalar的排序，或者直接用summation的pooling策略
## 2. [Spectual Networks and Deep locally connected Networks on Graphs](https://arxiv.org/pdf/1312.6203.pdf)
## 这篇文章首先介绍了CNN的在regular grid graph(诸如图片)上的特点：
### 1.Translation Structure，直接通过共享参数的filter instead of linear map(W)来进行输入转换
### 2.metric of the grid, 网格上做卷积操作？
### 3.muitiscale dyadic cluster(one hot?)可以通过利用pooling和stride来进行subsampling操作，同时也极大减小了input size，从而降低computational cost。
## 然后文章提出了两种构造图的方式，spatial construction和spectral construction。
### 1. spatial construction. 
