# 元素计数，使得左右子阵列之和之差等于 k 的倍数

> 原文:[https://www . geeksforgeeks . org/元素计数-左右子数组之和的差值等于 k 的倍数/](https://www.geeksforgeeks.org/count-of-elements-such-that-difference-between-sum-of-left-and-right-sub-arrays-is-equal-to-a-multiple-of-k/)

给定一个长度为 **n** 的数组**arr【】**和一个整数 **k** ，任务是在左右子数组之和之差等于给定数 k 的倍数的数组中找到从 2 到 n-1 的索引数

**示例:**

> **输入:** arr[] = {1，2，3，3，1，1}，k = 4
> **输出:** 2
> 说明:唯一可能的指数是 4 和 5
> 
> **输入:** arr[] = {1，2，3，4，5}，k = 1
> T3】输出: 3

**进场:**

*   创建包含左侧元素总和的前缀数组和包含右侧元素总和的后缀数组。
*   检查每一个索引左边和右边和的差，如果它能被 k 整除，就增加计数器。

下面是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ code to count of elements such that
// difference between the sum of left and right
// sub-arrays are equal to a multiple of k

#include <bits/stdc++.h>
using namespace std;

// Functions to find the no of elements
int noOfElement(int a[], int n, int k)
{
    // Creating a prefix array
    int prefix[n];

    // Starting element of prefix array
    // will be the first element
    // of given array
    prefix[0] = a[0];
    for (int i = 1; i < n; i++) {
        prefix[i] = prefix[i - 1] + a[i];
    }

    // Creating a suffix array;
    int suffix[n];
    // Last element of suffix array will
    // be the last element of given array
    suffix[n - 1] = a[n - 1];
    for (int i = n - 2; i >= 0; i--) {
        suffix[i] = suffix[i + 1] + a[i];
    }

    // Checking difference of left and right half
    // is divisible by k or not.
    int cnt = 0;
    for (int i = 1; i < n - 1; i++) {
        if ((prefix[i] - suffix[i]) % k == 0
            || (suffix[i] - prefix[i]) % k == 0) {
            cnt = cnt + 1;
        }
    }

    return cnt;
}

// Driver code
int main()
{
    int a[] = { 1, 2, 3, 3, 1, 1 };
    int k = 4;
    int n = sizeof(a) / sizeof(a[0]);
    cout << noOfElement(a, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to count of elements such that
// difference between the sum of left and right
// sub-arrays are equal to a multiple of k
class GFG
{

// Functions to find the no of elements
static int noOfElement(int a[], int n, int k)
{
    // Creating a prefix array
    int []prefix = new int[n];

    // Starting element of prefix array
    // will be the first element
    // of given array
    prefix[0] = a[0];
    for (int i = 1; i < n; i++)
    {
        prefix[i] = prefix[i - 1] + a[i];
    }

    // Creating a suffix array;
    int []suffix = new int[n];

    // Last element of suffix array will
    // be the last element of given array
    suffix[n - 1] = a[n - 1];
    for (int i = n - 2; i >= 0; i--)
    {
        suffix[i] = suffix[i + 1] + a[i];
    }

    // Checking difference of left and right half
    // is divisible by k or not.
    int cnt = 0;
    for (int i = 1; i < n - 1; i++)
    {
        if ((prefix[i] - suffix[i]) % k == 0
            || (suffix[i] - prefix[i]) % k == 0)
        {
            cnt = cnt + 1;
        }
    }
    return cnt;
}

// Driver code
public static void main(String[] args)
{
    int a[] = { 1, 2, 3, 3, 1, 1 };
    int k = 4;
    int n = a.length;
    System.out.print(noOfElement(a, n, k));
}
}

// This code is contributed by Rajput-Ji
```

## 计算机编程语言

```
# Python3 code to count of elements such that
# difference between the sum of left and right
# sub-arrays are equal to a multiple of k

# Functions to find the no of elements
def noOfElement(a, n, k):

    # Creating a prefix array
    prefix = [0] * n

    # Starting element of prefix array
    # will be the first element
    # of given array
    prefix[0] = a[0]
    for i in range(1, n):
        prefix[i] = prefix[i - 1] + a[i]

    # Creating a suffix array
    suffix = [0] * n

    # Last element of suffix array will
    # be the last element of given array
    suffix[n - 1] = a[n - 1]
    for i in range(n - 2, -1, -1):
        suffix[i] = suffix[i + 1] + a[i]

    # Checking difference of left and right half
    # is divisible by k or not.
    cnt = 0
    for i in range(1, n - 1):
        if ((prefix[i] - suffix[i]) % k == 0 or (suffix[i] - prefix[i]) % k == 0):
            cnt = cnt + 1

    return cnt

# Driver code

a = [ 1, 2, 3, 3, 1, 1 ]
k = 4
n = len(a)
print(noOfElement(a, n, k))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# code to count of elements such that
// difference between the sum of left and right
// sub-arrays are equal to a multiple of k
using System;

class GFG
{

    // Functions to find the no of elements
    static int noOfElement(int []a, int n, int k)
    {
        // Creating a prefix array
        int []prefix = new int[n];

        // Starting element of prefix array
        // will be the first element
        // of given array
        prefix[0] = a[0];
        for (int i = 1; i < n; i++)
        {
            prefix[i] = prefix[i - 1] + a[i];
        }

        // Creating a suffix array;
        int []suffix = new int[n];

        // Last element of suffix array will
        // be the last element of given array
        suffix[n - 1] = a[n - 1];
        for (int i = n - 2; i >= 0; i--)
        {
            suffix[i] = suffix[i + 1] + a[i];
        }

        // Checking difference of left and right half
        // is divisible by k or not.
        int cnt = 0;
        for (int i = 1; i < n - 1; i++)
        {
            if ((prefix[i] - suffix[i]) % k == 0
                || (suffix[i] - prefix[i]) % k == 0)
            {
                cnt = cnt + 1;
            }
        }
        return cnt;
    }

    // Driver code
    public static void Main()
    {
        int []a = { 1, 2, 3, 3, 1, 1 };
        int k = 4;
        int n = a.Length;
        Console.Write(noOfElement(a, n, k));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// Javascript code to count of elements such that
// difference between the sum of left and right
// sub-arrays are equal to a multiple of k

// Functions to find the no of elements
function noOfElement(a,n,k)
{
    // Creating a prefix array
    let prefix = new Array(n);

    // Starting element of prefix array
    // will be the first element
    // of given array
    prefix[0] = a[0];
    for (let i = 1; i < n; i++)
    {
        prefix[i] = prefix[i - 1] + a[i];
    }

    // Creating a suffix array;
    let suffix = new Array(n);

    // Last element of suffix array will
    // be the last element of given array
    suffix[n - 1] = a[n - 1];
    for (let i = n - 2; i >= 0; i--)
    {
        suffix[i] = suffix[i + 1] + a[i];
    }

    // Checking difference of left and right half
    // is divisible by k or not.
    let cnt = 0;
    for (let i = 1; i < n - 1; i++)
    {
        if ((prefix[i] - suffix[i]) % k == 0
            || (suffix[i] - prefix[i]) % k == 0)
        {
            cnt = cnt + 1;
        }
    }
    return cnt;
}

    // Driver code   
    let a=[1, 2, 3, 3, 1, 1];
    let k = 4;
    let n = a.length;
    document.write(noOfElement(a, n, k));

// This code is contributed by patel2127
</script>
```

**Output:** 

```
2
```