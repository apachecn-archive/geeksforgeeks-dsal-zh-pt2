# 给定数组中最多替换一个元素后的最大可能 GCD

> 原文:[https://www . geeksforgeeks . org/给定数组中最多替换一个元素后的最大可能 gcd/](https://www.geeksforgeeks.org/maximum-possible-gcd-after-replacing-at-most-one-element-in-the-given-array/)

给定一个大小为 **N > 1** 的数组 **arr[]** 。任务是通过最多替换一个元素来找到数组的最大可能 [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 。
**举例:**

> **输入:** arr[] = {6，7，8}
> **输出:** 2
> 将 7 替换为 2，gcd(6，2，8) = 2
> ，这是最大可能。
> **输入:** arr[] = {12，18，30}
> **输出:** 6

**进场:**

*   想法是找到所有长度为**(N–1)**的子序列的 GCD 值，并移除子序列中必须被替换的元素，因为它可以被子序列中已经存在的任何其他元素替换。找到的最大 GCD 将是答案。
*   为了最佳地找到子序列的 GCD，使用单状态[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)保持一个**前缀 GCD[]** 和一个**后缀 GCD[]** 数组。
*   **GCD 的最大值(prefixGCD[I–1]，sufixgcd[I+1])**为必选项。还要注意的是**后缀【1】**和**前缀【N–2】**也需要进行比较，以防第一个或最后一个元素需要替换。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum
// possible gcd after replacing
// a single element
int MaxGCD(int a[], int n)
{

    // Prefix and Suffix arrays
    int Prefix[n + 2];
    int Suffix[n + 2];

    // Single state dynamic programming relation
    // for storing gcd of first i elements
    // from the left in Prefix[i]
    Prefix[1] = a[0];
    for (int i = 2; i <= n; i += 1) {
        Prefix[i] = __gcd(Prefix[i - 1], a[i - 1]);
    }

    // Initializing Suffix array
    Suffix[n] = a[n - 1];

    // Single state dynamic programming relation
    // for storing gcd of all the elements having
    // index greater than or equal to i in Suffix[i]
    for (int i = n - 1; i >= 1; i -= 1) {
        Suffix[i] = __gcd(Suffix[i + 1], a[i - 1]);
    }

    // If first or last element of
    // the array has to be replaced
    int ans = max(Suffix[2], Prefix[n - 1]);

    // If any other element is replaced
    for (int i = 2; i < n; i += 1) {
        ans = max(ans, __gcd(Prefix[i - 1], Suffix[i + 1]));
    }

    // Return the maximized gcd
    return ans;
}

// Driver code
int main()
{
    int a[] = { 6, 7, 8 };
    int n = sizeof(a) / sizeof(a[0]);

    cout << MaxGCD(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the maximum
// possible gcd after replacing
// a single element
static int MaxGCD(int a[], int n)
{

    // Prefix and Suffix arrays
    int []Prefix = new int[n + 2];
    int []Suffix = new int[n + 2];

    // Single state dynamic programming relation
    // for storing gcd of first i elements
    // from the left in Prefix[i]
    Prefix[1] = a[0];
    for (int i = 2; i <= n; i += 1)
    {
        Prefix[i] = __gcd(Prefix[i - 1],
                               a[i - 1]);
    }

    // Initializing Suffix array
    Suffix[n] = a[n - 1];

    // Single state dynamic programming relation
    // for storing gcd of all the elements having
    // index greater than or equal to i in Suffix[i]
    for (int i = n - 1; i >= 1; i -= 1)
    {
        Suffix[i] = __gcd(Suffix[i + 1],
                               a[i - 1]);
    }

    // If first or last element of
    // the array has to be replaced
    int ans = Math.max(Suffix[2], Prefix[n - 1]);

    // If any other element is replaced
    for (int i = 2; i < n; i += 1)
    {
        ans = Math.max(ans, __gcd(Prefix[i - 1],
                                  Suffix[i + 1]));
    }

    // Return the maximized gcd
    return ans;
}

static int __gcd(int a, int b)
{
    return b == 0 ? a : __gcd(b, a % b);    
}

// Driver code
public static void main(String[] args)
{
    int a[] = { 6, 7, 8 };
    int n = a.length;

    System.out.println(MaxGCD(a, n));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import gcd as __gcd

# Function to return the maximum
# possible gcd after replacing
# a single element
def MaxGCD(a, n) :

    # Prefix and Suffix arrays
    Prefix = [0] * (n + 2);
    Suffix = [0] * (n + 2);

    # Single state dynamic programming relation
    # for storing gcd of first i elements
    # from the left in Prefix[i]
    Prefix[1] = a[0];

    for i in range(2, n + 1) :
        Prefix[i] = __gcd(Prefix[i - 1], a[i - 1]);

    # Initializing Suffix array
    Suffix[n] = a[n - 1];

    # Single state dynamic programming relation
    # for storing gcd of all the elements having
    # index greater than or equal to i in Suffix[i]
    for i in range(n - 1, 0, -1) :
        Suffix[i] = __gcd(Suffix[i + 1], a[i - 1]);

    # If first or last element of
    # the array has to be replaced
    ans = max(Suffix[2], Prefix[n - 1]);

    # If any other element is replaced
    for i in range(2, n) :
        ans = max(ans, __gcd(Prefix[i - 1],
                             Suffix[i + 1]));

    # Return the maximized gcd
    return ans;

# Driver code
if __name__ == "__main__" :

    a = [ 6, 7, 8 ];
    n = len(a);

    print(MaxGCD(a, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the maximum
// possible gcd after replacing
// a single element
static int MaxGCD(int []a, int n)
{

    // Prefix and Suffix arrays
    int []Prefix = new int[n + 2];
    int []Suffix = new int[n + 2];

    // Single state dynamic programming relation
    // for storing gcd of first i elements
    // from the left in Prefix[i]
    Prefix[1] = a[0];
    for (int i = 2; i <= n; i += 1)
    {
        Prefix[i] = __gcd(Prefix[i - 1],
                            a[i - 1]);
    }

    // Initializing Suffix array
    Suffix[n] = a[n - 1];

    // Single state dynamic programming relation
    // for storing gcd of all the elements having
    // index greater than or equal to i in Suffix[i]
    for (int i = n - 1; i >= 1; i -= 1)
    {
        Suffix[i] = __gcd(Suffix[i + 1],
                            a[i - 1]);
    }

    // If first or last element of
    // the array has to be replaced
    int ans = Math.Max(Suffix[2], Prefix[n - 1]);

    // If any other element is replaced
    for (int i = 2; i < n; i += 1)
    {
        ans = Math.Max(ans, __gcd(Prefix[i - 1],
                                Suffix[i + 1]));
    }

    // Return the maximized gcd
    return ans;
}

static int __gcd(int a, int b)
{
    return b == 0 ? a : __gcd(b, a % b);    
}

// Driver code
public static void Main(String[] args)
{
    int []a = { 6, 7, 8 };
    int n = a.Length;

    Console.WriteLine(MaxGCD(a, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

function gcd(a, b) {
  if (b==0) {
    return a;
  }

  return gcd(b, a % b);
}
// Function to return the maximum
// possible gcd after replacing
// a single element
function MaxGCD(a, n)
{

    // Prefix and Suffix arrays
    var Prefix = Array(n + 2).fill(0);
    var Suffix = Array(n + 2).fill(0);

    var i;
    // Single state dynamic programming relation
    // for storing gcd of first i elements
    // from the left in Prefix[i]
    Prefix[1] = a[0];
    for (i = 2; i <= n; i++) {
        Prefix[i] = gcd(Prefix[i - 1], a[i - 1]);
    }

    // Initializing Suffix array
    Suffix[n] = a[n - 1];

    // Single state dynamic programming relation
    // for storing gcd of all the elements having
    // index greater than or equal to i in Suffix[i]
    for (i = n - 1; i >= 1; i--) {
        Suffix[i] = gcd(Suffix[i + 1], a[i - 1]);
    }

    // If first or last element of
    // the array has to be replaced
    var ans = Math.max(Suffix[2], Prefix[n - 1]);

    // If any other element is replaced
    for (i = 2; i < n; i++) {
        ans = Math.max(ans, gcd(Prefix[i - 1],
        Suffix[i + 1]));
    }

    // Return the maximized gcd
    return ans;
}

// Driver code
    var a = [6, 7, 8];
    n = a.length;

    document.write(MaxGCD(a, n));

</script>
```

**Output:** 

```
2
```