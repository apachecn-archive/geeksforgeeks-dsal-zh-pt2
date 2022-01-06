# 跳 1 到 N

计算到达第 N 级楼梯的路数

> 原文:[https://www . geeksforgeeks . org/count-到达第 n 级的途径数-采取 1 到 n 的跳跃/](https://www.geeksforgeeks.org/count-the-number-of-ways-to-reach-nth-stair-by-taking-jumps-of-1-to-n/)

给定一个描述楼梯数量的整数 **N** ，任务是计算通过 1 到 N 的跳跃到达第 N 个<sup>楼梯</sup>的方法数量

**示例:**

> **输入:** N = 2
> **输出:** 2
> **说明:**两种到达方式为:(1，1) & (2)
> 
> **输入:**N = 3
> T3】输出: 4
> 
> **输入:**N = 4
> T3】输出: 8

**方法:**在这个问题中，到达**I<sup>th</sup>T5】楼梯的方法数量为:**

> **到达 i <sup>第</sup>级楼梯=(到达 1 至 i-1 级楼梯的方式之和)+1**
> 至于在 **i** 、 **i <sup>第</sup>T10】级楼梯之前的任何一级楼梯都可以单跳到达。和 **+1** 直接跳到 **i** 。**

现在要解决这个问题:

1.  创建一个变量**和**来存储到达特定楼梯的路数。用 **0** 初始化。
2.  运行从 **i=1** 到 **i=N-1** 的循环，对于每次迭代:
    1.  创建一个变量，比如 **cur** 来存储到当前楼梯的路数。所以， **cur = sum + 1** 。
    2.  将**总和**改为**总和=总和+ cur** 。
3.  循环结束后返回 **sum + 1** 作为这个问题的答案。

下面是上述方法的实现:

## C++

```
// C++ code for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the number of ways
// to reach Nth stair
int findWays(int N)
{

    int sum = 0;
    for (int i = 1; i < N; i++) {
        int cur = sum + 1;
        sum += cur;
    }

    return sum + 1;
}

// Driver Code
int main()
{
    int N = 10;
    cout << findWays(N);
}
```

**Output**

```
512
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)