# 根据给定条件可能的二进制字符串的计数

> 原文:[https://www . geesforgeks . org/按给定条件计算二进制字符串的数量/](https://www.geeksforgeeks.org/count-of-binary-strings-possible-as-per-given-conditions/)

给定两个整数 **N** 和 **M** ，其中 **N** 表示**“0”**和 **M** 表示**“1”**的计数，以及一个整数 **K** ，任务是找出以下两种类型可以生成的最大二进制字符串数:

*   一根弦可以由 **K** ' **0** 和一根单根的 **1** 组成。
*   一根弦可以由**K****1**和一根单根的 **0** 组成。

**示例:**

> **输入:** N = 4，M = 4，K = 2
> **输出:** 6
> **解释:**
> 计数的“**0”**s = 4
> 计数的“**1”**s = 4
> 在给定约束条件下组合 0 和 1 的可能方式有{“001”、“001”}或{“001”、“110”}或{ }
> 每个组合可以用 **K + 1** 的方式排列，即“001”可以重新排列形成“010”，也可以组成“100”。
> 因此，可以生成的最大可能字符串为 3 * 2 = 6
> 
> **输入:** N = 101，M = 231，K = 15
> T3】输出: 320

**方法:**
按照以下步骤解决问题:

*   考虑以下三个条件来生成最大可能的二进制字符串组合:
    *   组合数不能超过 **N** 。
    *   组合数不能超过 **M** 。
    *   组合数不能超过 **(A+B)/(K + 1)** 。
*   因此，最大可能组合为 **min(A，B，(A + B)/ (K + 1))** 。
*   因此，可以生成的最大可能字符串为 **(K + 1) * min(A，B，(A + B)/ (K + 1))** 。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to generate maximum
// possible strings that can be generated
long long countStrings(long long A,
                    long long B,
                    long long K)
{

    long long X = (A + B) / (K + 1);

    // Maximum possible strings
    return (min(A, min(B, X)) * (K + 1));
}
int main()
{

    long long N = 101, M = 231, K = 15;
    cout << countStrings(N, M, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to generate maximum
// possible strings that can be generated
static long countStrings(long A, long B,
                        long K)
{
    long X = (A + B) / (K + 1);

    // Maximum possible strings
    return (Math.min(A, Math.min(B, X)) *
                                (K + 1));
}

// Driver Code
public static void main (String[] args)
{
    long N = 101, M = 231, K = 15;

    System.out.print(countStrings(N, M, K));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to implement 
# the above approach 

# Function to generate maximum 
# possible strings that can be
# generated 
def countStrings(A, B, K): 

    X = (A + B) // (K + 1) 

    # Maximum possible strings 
    return (min(A, min(B, X)) * (K + 1)) 

# Driver code
N, M, K = 101, 231, 15

print(countStrings(N, M, K))

# This code is contributed divyeshrabadiya07
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to generate maximum
// possible strings that can be generated
static long countStrings(long A, long B,
                        long K)
{
    long X = (A + B) / (K + 1);

    // Maximum possible strings
    return (Math.Min(A, Math.Min(B, X)) *
                                (K + 1));
}

// Driver Code
public static void Main (string[] args)
{
    long N = 101, M = 231, K = 15;

    Console.Write(countStrings(N, M, K));
}
}

// This code is contributed by rock_cool
```

## java 描述语言

```
<script>
// JavaScript Program to implement
// the above approach

// Function to generate maximum
// possible strings that can be generated
function countStrings(A, B, K)
{

    let X = Math.floor((A + B) / (K + 1));

    // Maximum possible strings
    return (Math.min(A, Math.min(B, X)) * (K + 1));
}

    let N = 101, M = 231, K = 15;
    document.write(countStrings(N, M, K));

// This code is contributed by Surbhi Tyagi.

</script>
```

**输出:**

```
320
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)