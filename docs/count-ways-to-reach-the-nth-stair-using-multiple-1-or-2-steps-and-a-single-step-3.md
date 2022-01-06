# 用多级 1 或 2 级和单级 3

计算到达第 n 级楼梯的方式

> 原文:[https://www . geesforgeks . org/count-way-to-th-stair-use-multi-1-或-2-steps-and-one-step-3/](https://www.geeksforgeeks.org/count-ways-to-reach-the-nth-stair-using-multiple-1-or-2-steps-and-a-single-step-3/)

给定一个整数 **N** 级楼梯，任务是计算到达 **N <sup>第</sup>T5】级楼梯的方法，通过走 1 步或 2 步任意次数，但正好走一次 3 步。
**举例:**** 

> **输入:** N = 4
> **输出:** 2
> **解释:**
> 因为 3 的一步必须强制进行，而且只能进行一次。所以，只有两种可能的方式:(1，3)或(3，1)
> **输入:** N = 5
> **输出:** 5
> **解释:**
> 到达第五级楼梯有五种可能的方式:(2，3)，(3，2)，(1，1，3)，(1，3，1)，(3，1，1)

**方法:**这个问题可以用[排列&组合](https://www.geeksforgeeks.org/permutation-and-combination/)的概念来解决。有一个限制，根据这个限制，一次只能走 3 步。这个想法是计算可能采取 3 个步骤的位置数量。
现在，下一个任务是找到移动到第 N <sup>级</sup>级的可能两步数，也就是(N–3)/2。这样，如果两步计数一次递增一次，所有可能的方法都将被覆盖，并且对于每一步，所有可能的组合都将被计算。
概括步骤后，每个可能序列的可能组合将是

```
Ways = (Length of sequence)! * (Count of 2-step)! 
       ------------------------------------------
                  (Count of 1-step)! 
```

**算法:**

*   将序列长度初始化为(N–2)。
*   将 1 步计数初始化为(N–3)。
*   将 2 步计数初始化为 0
*   将可能的 2 步计数初始化为(N-3)/2。
*   运行一个循环，直到 2 步的可能计数等于 2 步的实际计数。
    *   借助序列的当前长度、1 步计数、2 步计数和上面给出的公式，找出可能的方法数。
    *   将序列长度减少 1。
    *   将 2 步计数增加 1

下面是上述方法的实现。

## C++

```
// C++ implementation to find the number
// the number of ways to reach Nth stair
// by taking 1 or 2 steps at a time and
// 3rd step exactly once
#include <bits/stdc++.h>
using namespace std;

int factorial(int n)
{
    // Single line to find factorial
    return (n == 1 || n == 0) ? 1 :
            n * factorial(n - 1);
}

// Function to find
// the number of ways
int ways(int n)
{
    // Base Case
    if (n < 3)
    {
        return 0;
    }

    // Count of 2-steps
    int c2 = 0;

    // Count of 1-steps
    int c1 = n - 3;

    // Initial length of sequence
    int l = c1 + 1;
    int s = 0;

    // Expected count of 2-steps
    int exp_c2 = c1 / 2;

    // Loop to find the ways for
    // every possible sequence
    while (exp_c2 >= c2)
    {
        int f1 = factorial(l);
        int f2 = factorial(c1);
        int f3 = factorial(c2);
        int f4 = (f2 * f3);

        s += f1 / f4;
        c2 += 1;
        c1 -= 2;
        l -= 1;
    }
    return s;
}

// Driver code
int main()
{
    int n = 7;
    int ans = ways(n);

    cout << ans << endl;
    return 0;
}

// This code is contributed by coder001
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the number
// the number of ways to reach Nth stair
// by taking 1 or 2 steps at a time and
// 3rd step exactly once
class GFG {

static int factorial(int n)
{

    // Single line to find factorial
    return (n == 1 || n == 0) ? 1 :
            n * factorial(n - 1);
}

// Function to find
// the number of ways
static int ways(int n)
{

    // Base Case
    if (n < 3)
    {
        return 0;
    }

    // Count of 2-steps
    int c2 = 0;

    // Count of 1-steps
    int c1 = n - 3;

    // Initial length of sequence
    int l = c1 + 1;
    int s = 0;

    // Expected count of 2-steps
    int exp_c2 = c1 / 2;

    // Loop to find the ways for
    // every possible sequence
    while (exp_c2 >= c2)
    {
        int f1 = factorial(l);
        int f2 = factorial(c1);
        int f3 = factorial(c2);
        int f4 = (f2 * f3);

        s += f1 / f4;
        c2 += 1;
        c1 -= 2;
         l -= 1;
    }
    return s;
}

// Driver Code
public static void main(String args[])
{
    int n = 7;
    int ans = ways(n);

    System.out.println(ans);
}
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# Python3 implementation to find the number
# the number of ways to reach Nth stair
# by taking 1 or 2 steps at a time and
# 3rd Step exactly once

import math

# Function to find
# the number of ways
def ways(n):

    # Base Case
    if n < 3:
        return 0

    # Count of 2-steps
    c2 = 0

    # Count of 1-steps
    c1 = n-3

    # Initial length of sequence
    l = c1 + 1
    s = 0

    # expected count of 2-steps
    exp_c2 = c1 / 2

    # Loop to find the ways for
    # every possible sequence
    while exp_c2 >= c2:
        f1 = math.factorial(l)
        f2 = math.factorial(c1)
        f3 = math.factorial(c2)
        s += f1//(f2 * f3)
        c2 += 1
        c1 -= 2
        l -= 1
    return s

# Driver Code
if __name__ == "__main__":
    N = 7
    print(ways(N))
```

## C#

```
// C# implementation to find the number
// the number of ways to reach Nth stair
// by taking 1 or 2 steps at a time and
// 3rd step exactly once
using System;
class GFG{

static int factorial(int n)
{

    // Single line to find factorial
    return (n == 1 || n == 0) ? 1 :
            n * factorial(n - 1);
}

// Function to find
// the number of ways
static int ways(int n)
{

    // Base Case
    if (n < 3)
    {
        return 0;
    }

    // Count of 2-steps
    int c2 = 0;

    // Count of 1-steps
    int c1 = n - 3;

    // Initial length of sequence
    int l = c1 + 1;
    int s = 0;

    // Expected count of 2-steps
    int exp_c2 = c1 / 2;

    // Loop to find the ways for
    // every possible sequence
    while (exp_c2 >= c2)
    {
        int f1 = factorial(l);
        int f2 = factorial(c1);
        int f3 = factorial(c2);
        int f4 = (f2 * f3);

        s += f1 / f4;
        c2 += 1;
        c1 -= 2;
        l -= 1;
    }
    return s;
}

// Driver code
static void Main()
{
    int n = 7;
    int ans = ways(n);

    Console.WriteLine(ans);
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>
// JavaScript implementation to find the number
// the number of ways to reach Nth stair
// by taking 1 or 2 steps at a time and
// 3rd step exactly once

function factorial(n)
{

    // Single line to find factorial
    return (n == 1 || n == 0) ? 1 :
            n * factorial(n - 1);
}

// Function to find
// the number of ways
function ways(n)
{
    // Base Case
    if (n < 3)
    {
        return 0;
    }

    // Count of 2-steps
    let c2 = 0;

    // Count of 1-steps
    let c1 = n - 3;

    // Initial length of sequence
    let l = c1 + 1;
    let s = 0;

    // Expected count of 2-steps
    let exp_c2 = Math.floor(c1 / 2);

    // Loop to find the ways for
    // every possible sequence
    while (exp_c2 >= c2)
    {
        let f1 = factorial(l);
        let f2 = factorial(c1);
        let f3 = factorial(c2);
        let f4 = (f2 * f3);

        s += Math.floor(f1 / f4);
        c2 += 1;
        c1 -= 2;
        l -= 1;
    }
    return s;
}

// Driver code
    let n = 7;
    let ans = ways(n);
    document.write(ans);

// This code is contributed by Surbhi Tyagi.
</script>
```

**Output:** 

```
20
```

**业绩分析:**

*   **时间复杂度:**和上面的方法一样，有一个循环来检查每一个可能上升(N-3)需要 O(N)时间的序列的可能排列，并找到需要 O(N)时间的可能组合，因此时间复杂度将是**O(N】<sup>2</sup>)**。
*   **空间复杂度:**和上面的方法一样，没有使用额外的空间，因此空间复杂度为 **O(1)** 。

**注意:**通过预先计算每个数字的阶乘直到 N，时间复杂度可以提高到 O(N)