# 当 N 除以 1 到 N+1 的所有正整数时，找出所有可能的余数

> 原文:[https://www . geeksforgeeks . org/find-所有可能的余数-当-n 被从-1 到-n1 的所有正整数除/](https://www.geeksforgeeks.org/find-all-the-possible-remainders-when-n-is-divided-by-all-positive-integers-from-1-to-n1/)

给定一个大整数 **N** ，当 **N** 除以从 **1** 到 **N + 1** 的所有正整数时，任务是找到所有可能的余数。

**示例:**

> **输入:** N = 5
> **输出:**0 1 2 5
> 5% 1 = 0
> 5% 2 = 1
> 5% 3 = 2
> 5% 4 = 1
> 5% 5 = 0
> 5% 6 = 5
> 
> **输入:**N = 11
> T3】输出: 0 1 2 3 5 11

**天真方法:**运行从 **1** 到 **N + 1** 的循环，并返回将 **N** 除以范围内任意整数时找到的所有唯一余数。但是这种方法对于更大的 **N** 值是无效的。

**高效方法:**可以观察到，答案的一部分总是包含介于 **0** 到 **ceil(sqrt(n))** 之间的数字。可以通过在 **N** 的较小值上运行朴素算法并检查得到的余数，或者通过求解公式 **ceil(N / k) = x** 或 **x ≤ (N / k) < x + 1** 来证明，其中 **x** 是所有整数的余数之一 **k** 当 **N** 除以 **k** 为【t2t
以上不等式的解法无非是从 **(N / (x + 1)，N/x)**的长度**N/x–N/(x+1)= N/(x<sup>2</sup>+x)**的整数 **k** 。因此，从 **k = 1** 迭代到 **ceil(sqrt(N))** 并存储所有唯一的 **N % k** 。上面的 **k** 大于 **ceil(sqrt(N))** 怎么办？它们将始终对应于值 **0 ≤ x < ceil(sqrt(N))** 。因此，再次开始存储从**N/(ceil(sqrt(N))–1**到 **0** 的余数，并返回包含所有可能余数的最终答案。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

typedef long long int ll;

// Function to find all the distinct
// remainders when n is divided by
// all the elements from
// the range [1, n + 1]
void findRemainders(ll n)
{

    // Set will be used to store
    // the remainders in order
    // to eliminate duplicates
    set<ll> vc;

    // Find the remainders
    for (ll i = 1; i <= ceil(sqrt(n)); i++)
        vc.insert(n / i);
    for (ll i = n / ceil(sqrt(n)) - 1; i >= 0; i--)
        vc.insert(i);

    // Print the contents of the set
    for (auto it : vc)
        cout << it << " ";
}

// Driver code
int main()
{
    ll n = 5;

    findRemainders(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to find all the distinct
// remainders when n is divided by
// all the elements from
// the range [1, n + 1]
static void findRemainders(long n)
{

    // Set will be used to store
    // the remainders in order
    // to eliminate duplicates
    HashSet<Long> vc = new HashSet<Long>();

    // Find the remainders
    for (long i = 1; i <= Math.ceil(Math.sqrt(n)); i++)
        vc.add(n / i);
    for (long i = (long) (n / Math.ceil(Math.sqrt(n)) - 1);
                                                i >= 0; i--)
        vc.add(i);

    // Print the contents of the set
    for (long it : vc)
        System.out.print(it+ " ");
}

// Driver code
public static void main(String[] args)
{
    long n = 5;

    findRemainders(n);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import ceil, floor, sqrt

# Function to find all the distinct
# remainders when n is divided by
# all the elements from
# the range [1, n + 1]
def findRemainders(n):

    # Set will be used to store
    # the remainders in order
    # to eliminate duplicates
    vc = dict()

    # Find the remainders
    for i in range(1, ceil(sqrt(n)) + 1):
        vc[n // i] = 1
    for i in range(n // ceil(sqrt(n)) - 1, -1, -1):
        vc[i] = 1

    # Print the contents of the set
    for it in sorted(vc):
        print(it, end = " ")

# Driver code
n = 5

findRemainders(n)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to find all the distinct
// remainders when n is divided by
// all the elements from
// the range [1, n + 1]
static void findRemainders(long n)
{

    // Set will be used to store
    // the remainders in order
    // to eliminate duplicates
    List<long> vc = new List<long>();

    // Find the remainders

    for (long i = 1; i <= Math.Ceiling(Math.Sqrt(n)); i++)
        vc.Add(n / i);
    for (long i = (long) (n / Math.Ceiling(Math.Sqrt(n)) - 1);
                                                 i >= 0; i--)
        vc.Add(i);
    vc.Reverse();

    // Print the contents of the set
    foreach (long it in vc)
        Console.Write(it + " ");
}

// Driver code
public static void Main(String[] args)
{
    long n = 5;

    findRemainders(n);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to find all the distinct
// remainders when n is divided by
// all the elements from
// the range [1, n + 1]
function findRemainders(n)
{

    // Set will be used to store
    // the remainders in order
    // to eliminate duplicates
    var vc = new Set();

    // Find the remainders
    for(var i = 1; i <= Math.ceil(Math.sqrt(n)); i++)
        vc.add(parseInt(n / i));
    for(var i = parseInt(n / Math.ceil(Math.sqrt(n))) - 1;
            i >= 0; i--)
        vc.add(i);

    // Print the contents of the set
    [...vc].sort((a, b) => a - b).forEach(it => {
        document.write(it + " ");
    });
}

// Driver code
var n = 5;

findRemainders(n);

// This code is contributed by famously

</script>
```

**Output:** 

```
0 1 2 5
```