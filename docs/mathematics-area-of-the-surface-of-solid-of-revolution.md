# 数学|旋转体表面面积

> 原文:[https://www . geesforgeks . org/数学-旋转固体表面面积/](https://www.geeksforgeeks.org/mathematics-area-of-the-surface-of-solid-of-revolution/)

考虑纵坐标 x=a 和 x=b 之间的 x-y 平面中的一个平面 y=f(x)，如果这条曲线的某一部分围绕一个轴旋转，则生成一个旋转体。
![](img/fdf8969c23f0ed4d0cbdcf21daf2fa7f.png)

**我们可以通过各种方式计算出这次公转的面积，比如:**

1.  **Cartesian Form:**
    *   **通过围绕 x 轴旋转曲线的圆弧而形成的实体面积是-**
        ![S= \int_{x=a}^{x=b} 2\pi y\sqrt{1+(\frac{dy}{dx})^2}dx](img/98801e276d86c39d53e5d596f4fb68f7.png "Rendered by QuickLaTeX.com")
    *   **绕 y 轴旋转曲线的旋转面积为-**
        ![S= \int_{y=c}^{y=d} 2\pi x \sqrt{1+(\frac{dx}{dy})^2}dy](img/0dbcc9b9ca5148103f1e2a9687f228a0.png "Rendered by QuickLaTeX.com")

2.  **Parametric Form: ![x=x(t), y=y(t)](img/1f2459563d7245b9f72376d7a66f70ff.png "Rendered by QuickLaTeX.com")**
    *   **关于 x 轴:**
        ![S=\int_{t=t_{1}}^{t=t_{2}} 2\pi y(t) \sqrt{(\frac{dx}{dt})^2+(\frac{dy}{dt})^2}dt](img/400a435276768fd9f10217e3cc09ae00.png "Rendered by QuickLaTeX.com")
    *   **关于 y 轴:**
        ![S=\int_{t=t_{1}}^{t=t_{2}} 2\pi x(t) \sqrt{(\frac{dx}{dt})^2+(\frac{dy}{dt})^2}dt](img/edaf35b519d9d673adf2e2bf7d1d7a81.png "Rendered by QuickLaTeX.com")
3.  **Polar Form: r=f(θ)**
    *   **关于 x 轴:初始线![ \theta = \frac{\pi}{2} ](img/9c8feff5cb6d62eaf215042e1f8e5ca6.png "Rendered by QuickLaTeX.com")** 
        ![S= \int_{\theta=\theta_1}^{\theta _2}2\pi y\frac{ds}{d\theta}d\theta](img/f8b850db6babbed5eeb3e51d7ef11aa7.png "Rendered by QuickLaTeX.com")
        ![=\int_{\theta=\theta_1}^{\theta _2}2\pi (r sin\theta) \sqrt{r^2+(\frac {dr}{d\theta})^2}d\theta ](img/a30b321b5f1fd5ca4ab7f51003a86630.png "Rendered by QuickLaTeX.com")
        这里用 f(θ)代替 r
    *   **关于 y 轴:**
        ![S= \int_{\theta=\theta_1}^{\theta _2}2\pi x\frac{ds}{d\theta}d\theta](img/03600a61c7e1d15fe3310222fb62b798.png "Rendered by QuickLaTeX.com")
        ![=\int_{\theta=\theta_1}^{\theta _2}2\pi (r cos\theta) \sqrt{r^2+(\frac {dr}{d\theta})^2}d\theta ](img/bcdfae97edd95ca914edd9e6cb5af45c.png "Rendered by QuickLaTeX.com")
        这里用 f(θ)代替 r
4.  **About any axis or line L: ![S= \int 2\pi (PM) ds](img/223295ba7e7f797ad24246d9702ab7c5.png "Rendered by QuickLaTeX.com") where PM is the perpendicular distance of a point P of the curve to the given axis.**
    *   **x 的界限:x = a 到 x = b**
        ![S=\int_{x=a}^{x=b} 2\pi (PM)\sqrt{1+(\frac{dy}{dx})^2}dx ](img/0c4d5e41c5a56b21af2cc98113a7fccb.png "Rendered by QuickLaTeX.com")
        这里 PM 是用 x 来表示的。
    *   **y 的界限:y = c 到 y = d**
        ![S= \int_{y=c}^{y=d} 2\pi (PM)\sqrt{1+(\frac{dx}{dy})^2}dy](img/03d3c71eb5391974db825d8986d1f515.png "Rendered by QuickLaTeX.com")
        这里 PM 是用 y 来表示的

    **例:**
    求抛物线![y^2=4ax, 0\leq x \leq 3a](img/bb975b195b47e39d4d902994f33babc1.png "Rendered by QuickLaTeX.com")绕 x 轴旋转产生的旋转体的面积。
    **解释:**
    现在给我们抛物线方程的笛卡尔形式，抛物线已经绕 x 轴旋转。因此，我们使用绕 x 轴旋转笛卡尔形式的公式，即:

    ![S= \int_{x=a}^{x=b} 2\pi y\sqrt{1+(\frac{dy}{dx})^2}dx](img/98801e276d86c39d53e5d596f4fb68f7.png "Rendered by QuickLaTeX.com")

    这里![y^2= 4ax](img/b3b92a3f813b36bca07ccd12bbf71dd6.png "Rendered by QuickLaTeX.com")。现在我们需要计算 dy/dx

    区分 w . r . t . x，我们得到:

    ![2yy'= 4a](img/b7165dda43c8c24d28a40d48c5dab6bb.png "Rendered by QuickLaTeX.com")

    ![y'=\frac{2a}{y} ](img/5e0e37647b2fdbec7edeb7ebfffc4a4d.png "Rendered by QuickLaTeX.com")

    ![1+(y')^2=1+\frac {4a^2}{y^2}=\frac{y^2+4a^2}{y^2}](img/e0712216572df294d9f0b3189d30b461.png "Rendered by QuickLaTeX.com")

    使用![y^2=4ax](img/63e81a655cafd13751440054d6252a20.png "Rendered by QuickLaTeX.com")

    ![\sqrt {1+(y')^2}=\sqrt{\frac{4ax+4a^2}{y^2}}=\frac{2\sqrt a}{y}\sqrt {a+x}](img/bc06ebe2780d6c99334f227bdce4fe4c.png "Rendered by QuickLaTeX.com")

    现在我们得到了 x=0 到 x=3 的极限。将我们的计算值代入上述公式，我们得到:

    ![S=\int_{0}^{3a} 2\pi y.{\frac{2\sqrt a}{y}\sqrt {a+x}}dx ](img/124b5ef91122b0051288cc56a96f1a67.png "Rendered by QuickLaTeX.com")

    ![=2\pi\int_{0}^{3a} y.{\frac{2\sqrt a}{y}\sqrt {a+x}}dx ](img/b3a5e1a9f31698484da44f9e67cf4e92.png "Rendered by QuickLaTeX.com")

    ![=4\pi\sqrt a\int_{0}^{3a}\sqrt {a+x}](img/824ffe495eb3788ddd086a79bf68e408.png "Rendered by QuickLaTeX.com")

    ![=4\pi\sqrt a\int_{0}^{3a}\frac{2}{3}(x+a)^{3/2}\Biggr|_{0}^{3a}](img/9db834c42fdb717983b96a7a99502e8f.png "Rendered by QuickLaTeX.com")

    ![=\frac{8}{3}\pi\sqrt a ((4a)^{3/2}-(a)^{3/2})](img/b0c70e14d18da6f10496d8b05c637ab0.png "Rendered by QuickLaTeX.com")

    ![=\frac{8}{3}\pi\sqrt a.a^{3/2}(8-1)](img/407508853a67b6306823687a3a3ac3a7.png "Rendered by QuickLaTeX.com")

    ![=\frac{56\pi a^2}{3} sq. units](img/2e3c5246aa7d5f51b3aa8298d8c755fc.png "Rendered by QuickLaTeX.com")