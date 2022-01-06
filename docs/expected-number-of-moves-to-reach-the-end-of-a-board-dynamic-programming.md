# 到达棋盘末端的预期移动次数|动态编程

> 原文:[https://www . geeksforgeeks . org/预计到达板端的移动次数-动态编程/](https://www.geeksforgeeks.org/expected-number-of-moves-to-reach-the-end-of-a-board-dynamic-programming/)

给定一个从 **1** 到 **N** 的长度为 **N** 的线性棋盘，任务是找到到达棋盘的第 **N <sup>第</sup>T9】单元所需的预期移动次数，如果我们从编号为 **1** 的单元开始，在每一步我们掷出一个立方体骰子来决定下一个移动。此外，我们不能超越董事会的界限。**注意**预期的移动次数可以是小数。
**举例:**** 

> **输入:** N = 8
> **输出:** 7
> p1 = (1 / 6) | 1 步- > 6 步预计到达终点
> p2 = (1 / 6) | 2 步- > 6 步预计到达终点
> p3 = (1 / 6) | 3 步- > 6 步预计到达终点
> p4 = (1 / 6) | 4 步- > 6 步预计到达终点
> p5 = (1 / 6) | 5 步- > 6 步预计到达终点
> p6 = (1 / 6) | 6 步- > 6 步预计到达终点
> 如果我们相距 7 步，那么我们可以以相等的概率(即 1 / 6)以 1、2、3、4、5、6 步
> 结束。
> 看上面的模拟更好理解。
> DP[N–1]= DP[7]
> = 1+(DP[1]+DP[2]+DP[3]+DP[4]+DP[5]+DP[6])/6
> = 1+6 = 7
> **输入:** N = 10
> **输出:** 7.36111

**方法:**这个问题可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。要解决这个问题，首先要决定 DP 的状态。一种方法是使用当前单元格和第 **N <sup>th</sup>** 单元格之间的距离来定义 DP 的状态。这个距离就叫 **X** 吧。因此 **dp[X]** 可以定义为从 **1 <sup>st</sup>** 单元开始到达长度为 **X + 1** 的板的末端所需的预期步数。
因此，递归关系变为:

> DP[x]= 1+(DP[x–1]+DP[x–2]+DP[x–3]+DP[x–4]+DP[x–5]+DP[x–6])/6

现在，对于基本情况:

> dp[0] = 0
> 我们来试着计算一下 dp[1]。
> dp[1] = 1 + 5 * (dp[1]) / 6 + dp[0](为什么？这是因为(5 / 6)是它停留在 1 的概率。)
> dp[1] / 6 = 1(因为 dp[0] = 0)
> dp[1] = 6
> 同样，DP[1]= DP[2]= DP[3]= DP[4]= DP[5]= 6

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
#define maxSize 50
using namespace std;

// To store the states of dp
double dp[maxSize];

// To determine whether a state
// has been solved before
int v[maxSize];

// Function to return the count
double expectedSteps(int x)
{

    // Base cases
    if (x == 0)
        return 0;
    if (x <= 5)
        return 6;

    // If a state has been solved before
    // it won't be evaluated again
    if (v[x])
        return dp[x];

    v[x] = 1;

    // Recurrence relation
    dp[x] = 1 + (expectedSteps(x - 1) +
                 expectedSteps(x - 2) +
                 expectedSteps(x - 3) +
                 expectedSteps(x - 4) +
                 expectedSteps(x - 5) +
                 expectedSteps(x - 6)) / 6;
    return dp[x];
}

// Driver code
int main()
{
    int n = 10;

    cout << expectedSteps(n - 1);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
    static int maxSize = 50;

    // To store the states of dp
    static double dp[] = new double[maxSize];

    // To determine whether a state
    // has been solved before
    static int v[] = new int[maxSize];

    // Function to return the count
    static double expectedSteps(int x)
    {

        // Base cases
        if (x == 0)
            return 0;

        if (x <= 5)
            return 6;

        // If a state has been solved before
        // it won't be evaluated again
        if (v[x] == 1)
            return dp[x];

        v[x] = 1;

        // Recurrence relation
        dp[x] = 1 + (expectedSteps(x - 1) +
                     expectedSteps(x - 2) +
                     expectedSteps(x - 3) +
                     expectedSteps(x - 4) +
                     expectedSteps(x - 5) +
                     expectedSteps(x - 6)) / 6;

        return dp[x];
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 10;

        System.out.println(expectedSteps(n - 1));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach
maxSize = 50

# To store the states of dp
dp = [0] * maxSize

# To determine whether a state
# has been solved before
v = [0] * maxSize

# Function to return the count
def expectedSteps(x):

    # Base cases
    if (x == 0):
        return 0
    if (x <= 5):
        return 6

    # If a state has been solved before
    # it won't be evaluated again
    if (v[x]):
        return dp[x]

    v[x] = 1

    # Recurrence relation
    dp[x] = 1 + (expectedSteps(x - 1) +
                 expectedSteps(x - 2) +
                 expectedSteps(x - 3) +
                 expectedSteps(x - 4) +
                 expectedSteps(x - 5) +
                 expectedSteps(x - 6)) / 6
    return dp[x]

# Driver code
n = 10

print(round(expectedSteps(n - 1), 5))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    static int maxSize = 50;

    // To store the states of dp
    static double []dp = new double[maxSize];

    // To determine whether a state
    // has been solved before
    static int []v = new int[maxSize];

    // Function to return the count
    static double expectedSteps(int x)
    {

        // Base cases
        if (x == 0)
            return 0;

        if (x <= 5)
            return 6;

        // If a state has been solved before
        // it won't be evaluated again
        if (v[x] == 1)
            return dp[x];

        v[x] = 1;

        // Recurrence relation
        dp[x] = 1 + (expectedSteps(x - 1) +
                     expectedSteps(x - 2) +
                     expectedSteps(x - 3) +
                     expectedSteps(x - 4) +
                     expectedSteps(x - 5) +
                     expectedSteps(x - 6)) / 6;

        return dp[x];
    }

    // Driver code
    public static void Main ()
    {
        int n = 10;

        Console.WriteLine(expectedSteps(n - 1));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
var maxSize = 50;

// To store the states of dp
var dp = Array(maxSize);

// To determine whether a state
// has been solved before
var v = Array(maxSize);

// Function to return the count
function expectedSteps(x)
{

    // Base cases
    if (x == 0)
        return 0;
    if (x <= 5)
        return 6;

    // If a state has been solved before
    // it won't be evaluated again
    if (v[x])
        return dp[x];

    v[x] = 1;

    // Recurrence relation
    dp[x] = 1 + (expectedSteps(x - 1) +
                 expectedSteps(x - 2) +
                 expectedSteps(x - 3) +
                 expectedSteps(x - 4) +
                 expectedSteps(x - 5) +
                 expectedSteps(x - 6)) / 6;
    return dp[x];
}

// Driver code
var n = 10;
document.write( expectedSteps(n - 1).toFixed(5));

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
7.36111
```