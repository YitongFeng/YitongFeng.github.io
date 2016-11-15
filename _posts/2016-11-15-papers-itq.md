#Problem
Similarity-preserving binary codes for efficient retrieval in large-scale image collections.

#ITQ Method
##1. Dimensionality Reduction 
Such as PCA.
	
Ommited here.

##2.  Binary quantization
**symbols:**
$X\in \mathbb R^{n\times d} $: Data matrix, zero-centered data, i.e., $\sum_{i=1}^n x_i = 0$
$V \in \mathbb R^{n\times c}$:  Data matrix after dimensionality reduction.
$R\in \mathbb R^{c\times c}$: Rotation matrix
$B\in \{-1, 1\}^{n\times c}$ Binary code matrix we want.
$ v \in \mathbb R^c $: vector in the projected space (i.e. v is data after dimensionality reduction from raw data X. $v\in V$)

**Our goal:** Learn binary code B, which can keep more information of the original data, so we need to minimize the quantization loss.
Thus we get the loss function:
$$min\;( \,Q(B,R)=\parallel B-VR\parallel_F^2 \,)	\qquad(1)$$
V muiltiply R is for rotating the data to minimize the quantization loss. (Why multiply a matrix can rotate data see reference[2] )



##ITQ training process
Adopt a k-means-like iterative quantization (ITQ) procedure to
find a local minimum of the quantization loss. 
**(1) Fix R and update B**
In each iteration, each data point is first assigned to the nearest vertex of the binary hypercube.
expand (1): 
$$Q(B, R) \quad= \quad \left\| B \right\|_F^2  + \left\| V \right\|_F^2 - 2tr(BR^TV^T)$$
$$\qquad\qquad\qquad\qquad=\quad nc + \left\|V\right\|_F^2-2tr(BR^TV^T)\quad\qquad (2)$$	
V is fixed, minimizing(2) is equivalent to maximizing
$$tr(BR^TV^T=\sum_{i=1}^n\sum_{j=1}^cB_{ij}\tilde V_{ij}$$
Where $ V_{ij} = VR$.
To maximize (2), we need to have $B_{ij}=1$whenever  $V_{ij}\ge 0$and $-1$ otherwise.	i.e. $B=sgn(VR)$ 
**(2) Fix B and update R** 
Then R is updated to minimize the quantization loss given this assignment.
Solving process as follows:
1) Compute the SVD of the $c\times c$ matrix of $B^TV$ as $S\Omega \hat{S}^T$	
2) Let $R = \hat SS^T $
	


<br>
#Background Knowledge

**Frobenius范数：**![这里写图片描述](http://img.blog.csdn.net/20161115193610484)
**量化：**在数字信号处理领域，量化指将信号的连续取值（或者大量可能的离散取值）近似为有限多个（或较少的）离散值的过程。

**正交矩阵：**如果：AAT=E（E为单位矩阵，AT表示“矩阵A的转置矩阵”。）或ATA=E，则n阶实矩阵A称为正交矩阵， 若A为正交阵，则满足以下条件:

 1. AT是正交矩阵
 2. E为单位矩阵
 3. A的各行是单位向量且两两正交（向量正交即向量积为0）
 4. A的各列是单位向量且两两正交
 5. (Ax,Ay)=(x,y) x,y∈R
 6. |A| = 1或-1

**SVD分解：**

对任意M*N的矩阵均存在如下分解

![这里写图片描述](http://img.blog.csdn.net/20161106213314947)


#Reference
[1] [Yunchao Gong, Svetlana Lazebnik. Iterative Quantization: A Procrustean Approach to Learning Binary Codes (ITQ), 2011.](http://www.cs.unc.edu/~lazebnik/publications/cvpr11_small_code.pdf)
[2]http://blog.sina.com.cn/s/blog_4b16455701016aau.html
[3]http://www.cnblogs.com/LeftNotEasy/archive/2011/01/19/svd-and-applications.html





