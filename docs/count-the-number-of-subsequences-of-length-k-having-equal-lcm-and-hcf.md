# 计算长度为 k 且 LCM 和 HCF 相等的子序列的数量

> 原文:[https://www . geeksforgeeks . org/count-长度为 k 的子序列的数量具有相等的 lcm 和-hcf/](https://www.geeksforgeeks.org/count-the-number-of-subsequences-of-length-k-having-equal-lcm-and-hcf/)

给定一个数组 **Arr** 和一个整数 **K** 。任务是找到大小为 **K** 的子序列的数量，使得序列的 **LCM** 和 **HCF** 相同。
**举例:**

> **输入:** Arr = {1，2，2，3，3}，K = 2
> **输出:** 2
> 子序列为–{ 2，2}和{3，3}
> **输入:** Arr = {1，1，1，1，2，2}，K = 3
> **输出:** 4

**进场:**
**LCM** 和 **HCF** ( GCD)在一组数字全部相同时相等。
可以用以下方式证明。让我们举一个两个数的例子。
设两个数为 **x** 和 **y**
**HCF(x，y)** = **LCM(x，y)** = k(说)
自 **HCF(x，y) = k** ，
T22】x = kn 和， **y = km** ，对于某些自然数 **m【来说 **k<sup>2</sup>= km×kn**
由此可见， **mn = 1**
因此， **m = n = 1** ，由于 m、n 都是自然数
因此，
**x = kn = k** ，而， **y = km = k**
暗含， **x = y = k** ，即
这个概念可以扩展到一组数字。因此，证明了相同的数具有相等的 GCD 和 LCM。
之后，我们需要借助地图找到数组中每个元素的频率。然后，组合理论的公式将用于为给定频率的特定元素找到特定长度 K 的子序列的计数。这个概念将适用于所有给定频率的元素，所有元素的总和就是答案。
以下是上述方法的实施:** 

## C++

```
// C++ implementation
#include <bits/stdc++.h>
using namespace std;

// Returns factorial of n
long long fact(int n)
{
    long long res = 1;
    for (int i = 2; i <= n; i++)
        res = res * i;
    return res;
}

// Returns nCr for the
// given values of r and n
long long nCr(int n, int r)
{
    return fact(n) / (1LL * fact(r)
                      * fact(n - r));
}

long long number_of_subsequences(int arr[],
                                 int k,
                                 int n)
{

    long long s = 0;

    // Map to store the frequencies
    // of each elements
    map<int, int> m;

    // Loop to store the
    // frequencies of elements
    // in the map
    for (int i = 0; i < n; i++) {
        m[arr[i]]++;
    }

    for (auto j : m) {

        // Using nCR formula to
        // calculate the number
        // of subsequences of a
        // given length
        s = s + 1LL * nCr(j.second, k);
    }

    return s;
}

// Driver Code
int main()
{
    int arr[] = { 1, 1, 1, 1, 2, 2, 2 };
    int k = 2;
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function calling
    cout << number_of_subsequences(arr, k, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for above approach
import java.util.*;

class GFG
{

// Returns factorial of n
static long fact(int n)
{
    long res = 1;
    for (int i = 2; i <= n; i++)
        res = res * i;
    return res;
}

// Returns nCr for the
// given values of r and n
static long nCr(int n, int r)
{
    return fact(n) / (1 * fact(r) *
                          fact(n - r));
}

static long number_of_subsequences(int arr[],
                                   int k, int n)
{
    long s = 0;

    // Map to store the frequencies
    // of each elements
    HashMap<Integer,
            Integer> mp = new HashMap<Integer,
                                      Integer>();

    // Loop to store the
    // frequencies of elements
    // in the map
    for (int i = 0; i < n; i++)
    {
        if(mp.containsKey(arr[i]))
        {
            mp.put(arr[i], mp.get(arr[i]) + 1);
        }
        else
        {
            mp.put(arr[i], 1);
        }
    }

    for (Map.Entry<Integer,
                   Integer> j : mp.entrySet())
    {

        // Using nCR formula to
        // calculate the number
        // of subsequences of a
        // given length
        s = s + 1 * nCr(j.getValue(), k);
    }

    return s;
}

// Driver Code
static public void main ( String []arg)
{
    int arr[] = { 1, 1, 1, 1, 2, 2, 2 };
    int k = 2;
    int n = arr.length;

    // Function calling
    System.out.println(number_of_subsequences(arr, k, n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Returns factorial of n
def fact(n):
    res = 1
    for i in range(2, n + 1):
        res = res * i
    return res

# Returns nCr for the
# given values of r and n
def nCr(n, r):
    return fact(n) // (fact(r) * fact(n - r))

def number_of_subsequences(arr, k, n):

    s = 0

    # Map to store the frequencies
    # of each elements
    m = dict()

    # Loop to store the
    # frequencies of elements
    # in the map
    for i in arr:
        m[i] = m.get(i, 0) + 1

    for j in m:

        # Using nCR formula to
        # calculate the number
        # of subsequences of a
        # given length
        s = s + nCr(m[j], k)

    return s

# Driver Code
arr = [1, 1, 1, 1, 2, 2, 2]
k = 2
n = len(arr)

# Function calling
print(number_of_subsequences(arr, k, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation for above approach
using System;
using System.Collections.Generic;

public class GFG
{

// Returns factorial of n
static long fact(int n)
{
    long res = 1;
    for (int i = 2; i <= n; i++)
        res = res * i;
    return res;
}

// Returns nCr for the
// given values of r and n
static long nCr(int n, int r)
{
    return fact(n) / (1 * fact(r) *
                          fact(n - r));
}

static long number_of_subsequences(int []arr,
                                   int k, int n)
{
    long s = 0;

    // Map to store the frequencies
    // of each elements
    Dictionary<int,int> mp = new Dictionary<int,int>();
    // Loop to store the
    // frequencies of elements
    // in the map
    for (int i = 0 ; i < n; i++)
    {
        if(mp.ContainsKey(arr[i]))
        {
            var val = mp[arr[i]];
            mp.Remove(arr[i]);
            mp.Add(arr[i], val + 1);
        }
        else
        {
            mp.Add(arr[i], 1);
        }
    }

    foreach(KeyValuePair<int, int> j in mp)
    {

        // Using nCR formula to
        // calculate the number
        // of subsequences of a
        // given length
        s = s + 1 * nCr(j.Value, k);
    }

    return s;
}

// Driver Code
static public void Main ( String []arg)
{
    int []arr = { 1, 1, 1, 1, 2, 2, 2 };
    int k = 2;
    int n = arr.Length;

    // Function calling
    Console.Write(number_of_subsequences(arr, k, n));
}
}
// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation for above approach

// Returns factorial of n
function fact(n)
{
    let res = 1;
    for (let i = 2; i <= n; i++)
        res = res * i;
    return res;
}

// Returns nCr for the
// given values of r and n
function nCr(n,r)
{
    return fact(n) / (1 * fact(r) *
                          fact(n - r));
}

function number_of_subsequences(arr,k,n)
{
        let s = 0;

    // Map to store the frequencies
    // of each elements
    let mp = new Map();

    // Loop to store the
    // frequencies of elements
    // in the map
    for (let i = 0; i < n; i++)
    {
        if(mp.has(arr[i]))
        {
            mp.set(arr[i], mp.get(arr[i]) + 1);
        }
        else
        {
            mp.set(arr[i], 1);
        }
    }

    for (let [key, value] of mp.entries())
    {

        // Using nCR formula to
        // calculate the number
        // of subsequences of a
        // given length
        s = s + 1 * nCr(value, k);
    }

    return s;
}

// Driver Code
let arr = [1, 1, 1, 1, 2, 2, 2];
let k = 2;
let n = arr.length;

// Function calling
document.write(number_of_subsequences(arr, k, n));

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
9
```