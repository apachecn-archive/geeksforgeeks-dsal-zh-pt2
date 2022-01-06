# 隐函数的导数–连续性和可微性|第 12 课数学

> 原文:[https://www . geeksforgeeks . org/隐函数导数-连续性和可微性-类-12-数学/](https://www.geeksforgeeks.org/derivatives-of-implicit-functions-continuity-and-differentiability-class-12-maths/)

隐函数是特定变量不能表示为另一个变量的函数的函数。依赖于多个变量的函数。隐式微分帮助我们计算 y 相对于 x 的导数，而不需要求解 y 的给定方程，这可以通过使用链式法则来实现，链式法则帮助我们将 y 表示为 x 的函数。

隐式微分也可以用来计算曲线的斜率，因为我们不能遵循直接对函数 y = f(x)进行微分并将点的 x 坐标值放在 dy/dx 中来获得斜率的过程。相反，我们将不得不遵循隐式微分的过程并求解 dy/dx。

这里使用的隐式微分法是一种求未知量导数的通用技术。

**例**

> x<sup>2</sup>y<sup>2</sup>+xy<sup>2</sup>+e<sup>xy</sup>= ABC =常数

**上面的函数是隐函数，我们不能用 y 来表示 x，也不能用 x 来表示 y。**

## **隐函数的导数**

由于函数不能用一个特定的变量来表示，我们必须遵循一种不同的方法来求隐函数的导数:

在计算隐函数的导数时，我们的目标是求解 **dy/dx** 或取决于函数的任何高阶导数。要根据 x 和 y 求解 dy/dx，我们必须遵循某些步骤:

## **计算隐函数导数的步骤**

*   给定一个包含因变量 y 和自变量 x 的隐函数(或者反过来)。
*   根据自变量(可以是 x 或 y)对整个方程进行微分。
*   微分后，需要应用微分的链式法则。
*   求解 dy/dx(或 dx/dy)的合成方程，如果需要高阶导数，则再次微分。

“y 和 x 的某个函数等于别的什么”。知道 x 并不能帮助我们直接计算 y。例如，

> x<sup>2</sup>+y<sup>2</sup>= r<sup>2(</sup>隐函数)

> **关于 x 进行区分:**T2【d】(x<sup>2</sup>)/dx+d(y<sup>2</sup>)/dx = d(r<sup>2</sup>)/dx
> 
> 求解每个术语:
> 
> **使用幂法则** : d(x <sup>2</sup> ) / dx = 2x
> 
> **使用链式法则** : d(y <sup>2</sup> )/ dx = 2y dydx
> 
> r <sup>2</sup> 为常数，因此其导数为 0: d(r <sup>2</sup> )/ dx = 0
> 
> 这给了我们:
> 
> 2x+2 和 dy/dx = 0
> 
> 收集一侧的所有 dy/dx
> 
> y dy/dx =-x
> 
> dy/dx 求解:
> 
> dy/dx = −xy

## 隐函数导数的样本问题

**实施例 1。求方程隐式给出的函数 y(x)的一阶导数的表达式:x<sup>2</sup>y<sup>3</sup>–4y+3x<sup>3</sup>= 2。**

**解决方案:**

**步骤 1:根据 x 对给定的方程或函数进行微分。**

> x <sup>2</sup> 和<sup>3</sup>–4y+3x<sup>3</sup>= 2。
> 
> d(x<sup>【2】</sup>y<sup>【3】</sup>–4y+3x<sup>)/dx = d(2)/dx</sup>

**第二步:右边的导数将简单地为 0，因为它是一个常数。**

分化后的左手边:

> 2xy<sup>3</sup>+3x<sup>2</sup>和<sup>2</sup>* dy/dx–4 * dy/dx+9x<sup>2</sup>0。

**第三步:一边收集涉及 dy/dx 的条款，另一边取剩余条款，得到:**

> dy/dx * (3x <sup>2</sup> 和<sup>2</sup>–4)=-9x<sup>2</sup>–2xy<sup>3</sup>
> 
> dy/dx =–(9x<sup>2</sup>+2xy<sup>3</sup>)/(3x<sup>2</sup>和<sup>2</sup>–4)

**这是曲线上任意一点的一阶导数的表达式。这个表达式还帮助我们计算在曲线的点(x，y)处绘制的切线的斜率。**

**例 2。求 y 的一阶导数，隐式给出为:y–tan<sup>-1</sup>y = x .**

**解决方案:**

> d(y–tan<sup>1</sup>y)/dx = d(x)/dx。
> 
> dy/dx-(1/(1+y<sup>2</sup>)* dy/dx = 1
> 
> dy/dx = 1/(1/(1–1/(1+y<sup>2</sup>))
> 
> dy/dx = 1/y <sup>2</sup> + 1

**例 3。找到 dy/dx if x<sup>2</sup>y<sup>3</sup>xy = 10。**

**解决方案:**

> 2xy <sup>3</sup> + x <sup>2</sup> 。3y <sup>2</sup> 。dy/dx–y–x。dy/dx = 0
> 
> (3x2y<sup>2</sup>–x)。dy/dx = y–2xy<sup>3</sup>
> 
> dy/dx =(y–2xy<sup>3</sup>/(3x<sup>2</sup>和<sup>2</sup>–x)

**例 4。找到 dy/dx，如果 y = sinx + cosy**

**解决方案:**

> y–cosy = sinx
> 
> dy/dx + siny。dy/dx = cosx
> 
> dy/dx = cosx / （1 + 桶）

**实施例 5。求曲线 x <sup>2</sup> + y <sup>2</sup> = 25 在点(3，4)处的切线斜率。**

**解决方案:**

> **注意曲线切线的斜率是导数，关于 x 隐式微分，得到**

> 2x + 2y. dy/dx = 0
> 
> dy/dx = -x/y
> 
> 因此，在(3，4)处，y′= 3/4 = 3/4，切线在点(3，4)处的斜率为 3/4。