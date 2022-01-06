# 仅表示为 2、4 和 6 之和的数的可能排列的计数

> 原文:[https://www . geeksforgeeks . org/number 的可能排列计数-仅表示为 2s-4s 和 6s 的和/](https://www.geeksforgeeks.org/count-of-possible-permutations-of-a-number-represented-as-a-sum-of-2s-4s-and-6s-only/)

给定一个整数 **N** ，任务是找出 N 可以表示为 **2** s、 **4** s 和 **6** s 之和的排列数。
**注:**同一组合的不同排列也会计算在内。
**举例:**

> **输入:** N = 8
> **输出:** 7
> **解释:**可能的组合有:
> 2 2 2 2
> 4 4
> 4 2
> 2 2 4
> 2 4 2
> 2 6
> 6 2
> **输入:** N = 6
> **输出:** 4

**方法:**为了解决这个问题，我们采用了[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)方法:

*   由于可以相加达到 **N** 的可能数是 2、4、6，可以认为是基本情况。通过使用基本情况，可以计算更多的情况。
*   让我们考虑一个大小为 **N + 1** 的 **dp[]** 数组，它计算并存储每个索引 **i** 处仅使用 2、4、6 形成值 **i** 的可能方式。

> dp[2] = 1
> dp[4] = 2 { 4 可以表示为 2+2，4}
> dp[6] = 4 { 6 可以表示为 2+2+2，2+4，4+2，6 }
> DP[I]= DP[I-2]+DP[I-4]+DP[I–6]对于范围**【8，N】**
> 中 I 的所有偶数值

*   因此，dp[N]包含所需的答案。

以下是上述方法的实现:

## C++

```
// C++ code for above implementation

#include <bits/stdc++.h>
using namespace std;

// Returns number of ways
// to reach score n
int count(int n)
{
    // table[i] will store count
    // of solutions for value i.
    if (n == 2)
        return 1;
    else if (n == 4)
        return 2;
    else if (n == 6)
        return 4;

    int table[n + 1], i;

    // Initialize all table
    // values as 0
    for (i = 0; i < n + 1; i++)
        table[i] = 0;

    // Base case (If given value
    // is 0, 1, 2, or 4)
    table[0] = 0;
    table[2] = 1;
    table[4] = 2;
    table[6] = 4;

    for (i = 8; i <= n; i = i + 2) {

        table[i] = table[i - 2]
                   + table[i - 4]
                   + table[i - 6];
    }

    return table[n];
}

// Driver Code
int main(void)
{
    int n = 8;
    cout << count(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for above implementation
import java.util.*;
class GFG{

// Returns number of ways
// to reach score n
static int count(int n)
{
    // table[i] will store count
    // of solutions for value i.
    if (n == 2)
        return 1;
    else if (n == 4)
        return 2;
    else if (n == 6)
        return 4;

    int table[] = new int[n + 1];
    int i;

    // Initialize all table
    // values as 0
    for (i = 0; i < n + 1; i++)
        table[i] = 0;

    // Base case (If given value
    // is 0, 1, 2, or 4)
    table[0] = 0;
    table[2] = 1;
    table[4] = 2;
    table[6] = 4;

    for (i = 8; i <= n; i = i + 2)
    {
        table[i] = table[i - 2] +
                   table[i - 4] +
                   table[i - 6];
    }

    return table[n];
}

// Driver Code
public static void main(String args[])
{
    int n = 8;
    System.out.print(count(n));
}
}

// This code is contributed by Akanksha_Rai
```

## 蟒蛇 3

```
# Python3 code for above implementation

# Returns number of ways
# to reach score n
def count(n) :

    # table[i] will store count
    # of solutions for value i.
    if (n == 2) :
        return 1;
    elif (n == 4) :
        return 2;
    elif (n == 6) :
        return 4;

    table = [0] * (n + 1);

    # Initialize all table
    # values as 0
    for i in range(n + 1) :
        table[i] = 0;

    # Base case (If given value
    # is 0, 1, 2, or 4)
    table[0] = 0;
    table[2] = 1;
    table[4] = 2;
    table[6] = 4;

    for i in range(8 , n + 1, 2) :

        table[i] = table[i - 2] + \
                   table[i - 4] + \
                   table[i - 6];

    return table[n];

# Driver Code
if __name__ == "__main__" :

    n = 8;
    print(count(n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# code for above implementation
using System;
class GFG{

// Returns number of ways
// to reach score n
static int count(int n)
{
    // table[i] will store count
    // of solutions for value i.
    if (n == 2)
        return 1;
    else if (n == 4)
        return 2;
    else if (n == 6)
        return 4;

    int []table = new int[n + 1];
    int i;

    // Initialize all table
    // values as 0
    for (i = 0; i < n + 1; i++)
        table[i] = 0;

    // Base case (If given value
    // is 0, 1, 2, or 4)
    table[0] = 0;
    table[2] = 1;
    table[4] = 2;
    table[6] = 4;

    for (i = 8; i <= n; i = i + 2)
    {
        table[i] = table[i - 2] +
                   table[i - 4] +
                   table[i - 6];
    }

    return table[n];
}

// Driver Code
public static void Main()
{
    int n = 8;
    Console.Write(count(n));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

// Returns number of ways
// to reach score n
function count(n)
{
    // table[i] will store count
    // of solutions for value i.
    if (n == 2)
        return 1;
    else if (n == 4)
        return 2;
    else if (n == 6)
        return 4;

    let table = Array.from({length: n+1}, (_, i) => 0);
    let i;

    // Initialize all table
    // values as 0
    for (i = 0; i < n + 1; i++)
        table[i] = 0;

    // Base case (If given value
    // is 0, 1, 2, or 4)
    table[0] = 0;
    table[2] = 1;
    table[4] = 2;
    table[6] = 4;

    for (i = 8; i <= n; i = i + 2)
    {
        table[i] = table[i - 2] +
                   table[i - 4] +
                   table[i - 6];
    }

    return table[n];
}

  // Driver Code

    let n = 8;
    document.write(count(n));

 // This code is contributed by susmitakundugoaldanga.
</script>
```

**Output:** 

```
7
```

**时间复杂度:***O(N)*
T5】辅助空间复杂度: *O(N)*