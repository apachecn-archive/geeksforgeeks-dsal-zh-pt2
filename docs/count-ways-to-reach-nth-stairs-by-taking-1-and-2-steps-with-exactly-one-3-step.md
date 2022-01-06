# 计算到达第 n 级楼梯的方法，只需走 1 步和 2 步，精确到 3 步

> 原文:[https://www . geesforgeks . org/count-way-reach-n-steps-by-走 1 步和 2 步-正好一步-3 步/](https://www.geeksforgeeks.org/count-ways-to-reach-nth-stairs-by-taking-1-and-2-steps-with-exactly-one-3-step/)

给定一个表示楼梯数量的数字 **N** ，任务是通过多次走 1 步、2 步和一次走 3 步到达 **N <sup>第</sup>T5【楼梯】。
**举例:**** 

> **输入:** N = 4
> **输出:** 2
> **解释:**
> 由于 3 的一个步骤必须强制执行且只能执行一次，
> 只有两种可能的方式:(1，3)或(3，1)
> **输入:** N = 5
> **输出:** 5
> **解释:**
> 由于 3 的一个步骤必须执行

**方法:**这个问题可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。要到达第 N <sup>级</sup>楼梯，人员应在第(N–1)<sup>级</sup>、(N–2)<sup>级</sup>或第(N–3)<sup>级</sup>。因此，要从底部到达第 N <sup>级</sup>级楼梯，到达第(N–1)<sup>级</sup>级楼梯(仅包含 3 级台阶),到达第(N–2)<sup>级</sup>级台阶(仅包含 3 级台阶),到达第(N–3)<sup>级</sup>级台阶(不包含 3 级台阶)。
那么这个问题的递推关系就是–

> 包括 _3[i] =包括 _3[i-1] +包括 _3[i-2] +不包括 _ 包括[i-3]

而当一次不允许 3 个步数时的递归关系为

> not _ includes[I]= not _ includes[I–1]+not _ includes[I–2]

下面是上述方法的实现。

## C++

```
// C++ implementation to find the number
// the number of ways to reach Nth stair
// by taking 1, 2 step at a time and
// 3 Steps at a time exactly once.

#include <iostream>
using namespace std;

// Function to find the number
// the number of ways to reach Nth stair
int number_of_ways(int n)
{
    // Array including number
    // of ways that includes 3
    int includes_3[n + 1] = {};

    // Array including number of
    // ways that doesn't includes 3
    int not_includes_3[n + 1] = {};

    // Initially to reach 3 stairs by
    // taking 3 steps can be
    // reached by 1 way
    includes_3[3] = 1;

    not_includes_3[1] = 1;
    not_includes_3[2] = 2;
    not_includes_3[3] = 3;

    // Loop to find the number
    // the number of ways to reach Nth stair
    for (int i = 4; i <= n; i++) {
        includes_3[i]
            = includes_3[i - 1] + includes_3[i - 2] + not_includes_3[i - 3];
        not_includes_3[i]
            = not_includes_3[i - 1] + not_includes_3[i - 2];
    }
    return includes_3[n];
}

// Driver Code
int main()
{
    int n = 7;

    cout << number_of_ways(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the number
// the number of ways to reach Nth stair
// by taking 1, 2 step at a time and
// 3 Steps at a time exactly once.
class GFG
{

// Function to find the number
// the number of ways to reach Nth stair
static int number_of_ways(int n)
{
    // Array including number
    // of ways that includes 3
    int []includes_3 = new int[n + 1];

    // Array including number of
    // ways that doesn't includes 3
    int []not_includes_3 = new int[n + 1];

    // Initially to reach 3 stairs by
    // taking 3 steps can be
    // reached by 1 way
    includes_3[3] = 1;

    not_includes_3[1] = 1;
    not_includes_3[2] = 2;
    not_includes_3[3] = 3;

    // Loop to find the number
    // the number of ways to reach Nth stair
    for (int i = 4; i <= n; i++)
    {
        includes_3[i]
            = includes_3[i - 1] + includes_3[i - 2] +
               not_includes_3[i - 3];
        not_includes_3[i]
            = not_includes_3[i - 1] + not_includes_3[i - 2];
    }
    return includes_3[n];
}

// Driver Code
public static void main(String[] args)
{
    int n = 7;

    System.out.print(number_of_ways(n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation to find the number
# the number of ways to reach Nth stair
# by taking 1, 2 step at a time and
# 3 Steps at a time exactly once.

# Function to find the number
# the number of ways to reach Nth stair
def number_of_ways(n):

    # Array including number
    # of ways that includes 3
    includes_3 = [0]*(n + 1)

    # Array including number of
    # ways that doesn't includes 3
    not_includes_3 = [0] * (n + 1)

    # Initially to reach 3 stairs by
    # taking 3 steps can be
    # reached by 1 way
    includes_3[3] = 1

    not_includes_3[1] = 1
    not_includes_3[2] = 2
    not_includes_3[3] = 3

    # Loop to find the number
    # the number of ways to reach Nth stair
    for i in range(4, n + 1):
        includes_3[i] = includes_3[i - 1] + \
                        includes_3[i - 2] + \
                        not_includes_3[i - 3]
        not_includes_3[i] = not_includes_3[i - 1] + \
                           not_includes_3[i - 2]
    return includes_3[n]

# Driver Code
n = 7

print(number_of_ways(n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation to find the number
// the number of ways to reach Nth stair
// by taking 1, 2 step at a time and
// 3 Steps at a time exactly once.
using System;

class GFG
{

// Function to find the number
// the number of ways to reach Nth stair
static int number_of_ways(int n)
{
    // Array including number
    // of ways that includes 3
    int []includes_3 = new int[n + 1];

    // Array including number of
    // ways that doesn't includes 3
    int []not_includes_3 = new int[n + 1];

    // Initially to reach 3 stairs by
    // taking 3 steps can be
    // reached by 1 way
    includes_3[3] = 1;

    not_includes_3[1] = 1;
    not_includes_3[2] = 2;
    not_includes_3[3] = 3;

    // Loop to find the number
    // the number of ways to reach Nth stair
    for (int i = 4; i <= n; i++)
    {
        includes_3[i]
            = includes_3[i - 1] + includes_3[i - 2] +
            not_includes_3[i - 3];
        not_includes_3[i]
            = not_includes_3[i - 1] + not_includes_3[i - 2];
    }
    return includes_3[n];
}

// Driver Code
public static void Main(String[] args)
{
    int n = 7;

    Console.Write(number_of_ways(n));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript implementation to find the number
// the number of ways to reach Nth stair
// by taking 1, 2 step at a time and
// 3 Steps at a time exactly once.

// Function to find the number
// the number of ways to reach Nth stair
function number_of_ways(n)
{
    // Array including number
    // of ways that includes 3
    let includes_3 = new Uint8Array(n + 1);

    // Array including number of
    // ways that doesn't includes 3
    let not_includes_3 = new Uint8Array(n + 1);

    // Initially to reach 3 stairs by
    // taking 3 steps can be
    // reached by 1 way
    includes_3[3] = 1;

    not_includes_3[1] = 1;
    not_includes_3[2] = 2;
    not_includes_3[3] = 3;

    // Loop to find the number
    // the number of ways to reach Nth stair
    for (let i = 4; i <= n; i++) {
        includes_3[i]
            = includes_3[i - 1] + includes_3[i - 2] + not_includes_3[i - 3];
        not_includes_3[i]
            = not_includes_3[i - 1] + not_includes_3[i - 2];
    }
    return includes_3[n];
}

// Driver Code

    let n = 7;

    document.write(number_of_ways(n));

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
20
```

**类似文章:** [计算一次走 1、2 或 3 步到达第 n 级楼梯的方法](https://www.geeksforgeeks.org/count-ways-reach-nth-stair-using-step-1-2-3/)