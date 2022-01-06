# 矩阵中的特征空间和特征谱值

> 原文:[https://www . geesforgeks . org/特征空间和特征谱矩阵值/](https://www.geeksforgeeks.org/eigenspace-and-eigenspectrum-values-in-a-matrix/)

**先决条件:**

*   [数学|特征值和特征向量](https://www.geeksforgeeks.org/eigen-values-and-eigen-vectors/)
*   [矩阵乘法](https://en.wikipedia.org/wiki/Matrix_multiplication)
*   [矩阵的零空间和零性](https://www.geeksforgeeks.org/null-space-and-nullity-of-a-matrix/)

对于给定的矩阵 *A* ，与特征值![\lambda](img/73aa9bb7ff52ad1f2fda1ba95744b076.png "Rendered by QuickLaTeX.com")相关联的 *A* 的所有特征向量的集合跨越一个子空间，该子空间被称为 *A* 相对于![\lambda](img/73aa9bb7ff52ad1f2fda1ba95744b076.png "Rendered by QuickLaTeX.com")的**特征空间**，并且由![E_\lambda](img/9688f9b11330f8c3ce44300c86cdf855.png "Rendered by QuickLaTeX.com")表示。 *A* 的所有特征值的集合称为 *A* 的**特征谱**，或简称为谱。
如果![\lambda](img/73aa9bb7ff52ad1f2fda1ba95744b076.png "Rendered by QuickLaTeX.com")是 A 的特征值，那么对应的特征空间![E_\lambda](img/9688f9b11330f8c3ce44300c86cdf855.png "Rendered by QuickLaTeX.com")就是齐次线性方程组![(A-\lambda I)x = 0](img/35c2e20938388b522f0965bf3572b1d3.png "Rendered by QuickLaTeX.com")的解空间。几何上，对应于非零特征值的特征向量指向由线性映射拉伸的方向。特征值是它被拉伸的因子。如果特征值为负，则拉伸方向翻转。

除了已经在文章[数学|特征值和特征向量](https://www.geeksforgeeks.org/eigen-values-and-eigen-vectors/)中列出的属性之外，下面是特征值和特征向量的一些有用的属性。

*   矩阵 A 及其转置![A^{T}](img/0b4288f083a77a10a4bb9ec7849d3f47.png "Rendered by QuickLaTeX.com")具有相同的特征值，但不一定具有相同的特征向量。*   The eigenspace ![E_\lambda](img/9688f9b11330f8c3ce44300c86cdf855.png "Rendered by QuickLaTeX.com") is the null space of ![A - \lambda I](img/4d45ae32bc2f432bdd538f4520a0e2a8.png "Rendered by QuickLaTeX.com") since
    ![Ax = \lambda x](img/9043633541fe09fb9f017cf6ed2d6d41.png "Rendered by QuickLaTeX.com") ![\Longleftrightarrow](img/2cc956ffc60f22c145eb504723a4bebe.png "Rendered by QuickLaTeX.com") ![Ax - \lambda x = 0](img/78acd937337b94c6ac77e89ecd66b0cf.png "Rendered by QuickLaTeX.com") ![\Longleftrightarrow](img/2cc956ffc60f22c145eb504723a4bebe.png "Rendered by QuickLaTeX.com") ![(A - \lambda I)x = 0](img/fea8a4f55103b1b76a6ba5496917554f.png "Rendered by QuickLaTeX.com") ![\Longleftrightarrow](img/2cc956ffc60f22c145eb504723a4bebe.png "Rendered by QuickLaTeX.com") ![x\in ker(A - \lambda I)](img/b5566bfcae579ceab059a83454f576fe.png "Rendered by QuickLaTeX.com")

    **注:** ker 代表**内核**，是*空区*的别称。

    **计算特征值、特征向量和特征空间:**

    ```
    Consider given 2 X 2 matrix:

    Step 1: Characteristic polynomial and Eigenvalues.
    The characteristic polynomial is given by 
    det() 

    After we factorize the characteristic polynomial, we will get

    which gives eigenvalues as  and 

    Step 2: Eigenvectors and Eigenspaces
    We find the eigenvectors that correspond to these eigenvalues by looking 
    at vectors x such that 

    For  we obtain

    After solving the above homogeneous system of equations,
    we will obtain a solution space

    This eigenspace is one dimensional as it possesses a single basis vector.
    Similarly, we find eigenvector for  by solving
    the homogeneous system of equations

    This means any vector , where  
    such as  is an eigenvector with 
    eigenvalue 2\. This means eigenspace is given as 

    ```

    上例中的两个本征空间![E_5](img/9d79e1deaea82897fce5a7654472b2d4.png "Rendered by QuickLaTeX.com")和![E_2](img/c3f96de7275b396fad60172c455f0676.png "Rendered by QuickLaTeX.com")是一维的，因为它们都被一个向量跨越。然而，在其他情况下，我们可能有多个相同的特征向量，并且特征空间可能有多个维度。