# 获得 N 个连续头部的预期试验次数

> 原文:[https://www . geeksforgeeks . org/预计连续 n 头试验次数/](https://www.geeksforgeeks.org/expected-number-of-trials-to-get-n-consecutive-heads/)

给定一个数字 **N** 。任务是找到一枚硬币必须被翻转的预期次数，以连续获得 **N** 头像。
**例:**

> **输入:** N = 2
> **输出:** 6
> **输入:** N = 5
> **输出:** 62

**进场:**
关键是观察如果我们在任何连续 **N** 翻转之间看到一个尾巴，它会打破连续头部的连胜，我们必须为 **N** 连续头部重新开始。
让期望的试次数为 **X** 得到 **N** 个连续头。以下是可能的情况:

*   **案例 1:** 如果在**第一次审判**中出现了尾巴，那么这意味着我们浪费了一次审判，我们将不得不进行 **X** 更多的审判来获得 **N** 连续的人头。该事件发生的概率为 **1/2** ，获得 **N** 个连续人头所需的试举总数为 **(X +前一次试举浪费的次数)**。
*   **案例 2:** 如果在**第二次审判**中出现了尾巴，那么这意味着我们浪费了之前所有的审判，我们将不得不进行 **X** 更多的审判来获得 **N** 连续的人头。该事件发生的概率为 **1/4** ，获得 **N** 个连续空翻所需的试跳总数为(X +浪费的前一次试跳次数)。
*   **案例 3:** 如果在**第三次审判**中出现了尾巴，那么这意味着我们已经浪费了之前所有的审判，我们将不得不进行 **X** 更多的审判来获得 **N** 。本次事件发生的概率为 **1/8** ，获得 **N** 次连续空翻所需的试跳总数为 **(X +前一次试跳浪费的次数)**。这将持续到我们连续获得 **N** 个磁头。
*   **案例 N:** 同样，如果在**第 N 次审判**中，出现了一条尾巴，那么就意味着我们浪费了之前所有的审判，我们将不得不做 **X** 更多的审判来获得 **N** 。该事件发生的概率为 **1/2 <sup>N</sup>** ，获得 **N** 次连续空翻所需的试跳总数为**(前一次试跳浪费的 X +计数)**。

从上述情况来看，所有概率的总和将给出 **N 个连续头部**的试验计数。数学上:

> X =(1/2)*(X+1)+(1/4)*(X+2)+(1/8)*(X+3)+。。。+(1/2<sup>N</sup>)*(X+N)+(1/2<sup>N</sup>)* N

对 x 求解上述方程，我们有:

```
By opening the above expressions and arranging it we have:
X = X(1/2 + 1/4 + 1/8 + . . . . . . 1/2N) 
    + (1/2 + 2/4 + 3/8 . . . . . . . + N/2N 
    + N/2N)
```

上述方程的第一部分形成几何级数，上述方程的第二部分形成算术几何序列。分别求解以上序列我们有:
为 [**几何序列:**](https://www.geeksforgeeks.org/geometric-progression/)

> GP 系列之和= 1/2 + 1/4 + 1/8 +。。。。。。1/2 <sup>N</sup>
> 第一项(a)是 1/2
> 公比(r)是 1/2
> 最后一项(第 N 项)是 1/2 <sup>N</sup> 也是* r <sup>N-1</sup>
> 因此总和由下式给出:
> GP 系列之和=(1/2)*((1 –( 1/2)<sup>N</sup>)/(1–1/2))使用公式:(a *(2)

对于 [**算术几何序列**](https://www.geeksforgeeks.org/sum-arithmetic-geometric-sequence/) :

> 设 S =算术几何数列之和:
> = > S = (1/2 + 2/4 + 3/8 +。。。。。。N/2 <sup>N</sup> ) ……。(1)
> 乘以 2，得到
> = > 2S = (1 + 2/2 + 3/4 +)。。。。。。。+ N/2 <sup>N-1</sup> ) ……。(2)
> 从等式(2)中减去等式(1)，我们得到
> = > S = (1/2 + 1/4 + 1/8 +。。。。。。1/2<sup>N-1</sup>)–N/2<sup>N</sup>T13】=>S = GP 系列之和–N/2<sup>N</sup>T16】=>S =(2 –( 1/2)<sup>N-1</sup>)–N/2<sup>N</sup>T21】

使用 GP 级数和算术几何序列的和:

> = > X = X *(1 –( 1/2)<sup>N</sup>)+(2–(1/2)<sup>N-1</sup>)–N/2<sup>N</sup>+N/2<sup>N
> =>X = X *(1–(1/2)<sup>N</sup>)+(2–(1/2)<sup>N-1</sup>)
> =>X *(1)</sup>

现在上面的 **X** 的公式给出了需要获得 **N 个连续人头**的试验次数。
以下是上述方法的实施:

## C++

```
// C++ implementation of the above approach
#include "bits/stdc++.h"
using namespace std;

// Driver Code
int main()
{
    int N = 3;

    // Formula for number of trails for
    // N consecutive heads
    cout << pow(2, N + 1) - 2;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG{

// Driver Code
public static void main(String[] args)
{
    int N = 3;

    // Formula for number of trails for
    // N consecutive heads
    System.out.print(Math.pow(2, N + 1) - 2);
}
}

// This code is contributed
// by shivanisinghss2110
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Driver code
if __name__ == '__main__':

    N = 3

    # Formula for number of trails for
    # N consecutive heads
    print(pow(2, N + 1) - 2)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the above approach
using System;
class GFG{

// Driver Code
public static void Main()
{
    int N = 3;

    // Formula for number of trails for
    // N consecutive heads
    Console.Write(Math.Pow(2, N + 1) - 2);
}
}

// This code is contributed
// by Code_Mech
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Driver Code

    let N = 3;

    // Formula for number of trails for
    // N consecutive heads
    document.write(Math.pow(2, N + 1) - 2);

</script>
```

**Output:** 

```
14
```

**时间复杂度:** O(1)