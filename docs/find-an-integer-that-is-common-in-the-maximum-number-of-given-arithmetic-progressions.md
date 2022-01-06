# 找出给定算术级数最大值中常见的整数

> 原文:[https://www . geeksforgeeks . org/find-给定算术级数的最大公约数/](https://www.geeksforgeeks.org/find-an-integer-that-is-common-in-the-maximum-number-of-given-arithmetic-progressions/)

给定两个整数数组 **A[]** 和 **D[]** ，其中*T5】A<sub>I</sub>*和 ***D <sub>i</sub>*** 分别表示一个[等差数列](https://www.geeksforgeeks.org/arithmetic-progression/)的第一个元素和公共差，任务是找到给定等差数列最大数目的公共元素。
**例:**

> **输入:** A[] = {3，1，2，5}，D[] = {2，3，1，2}
> **输出:** 7
> **解释:**整数 7 存在于所有给定的接入点中。
> **输入:** A[] = {13，1，2，5}，D[] = {5，10，1，12}
> **输出:** 41

**方法:**使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)可以轻松解决问题。初始化一个 ***cnt[]*** 阵列。对于每个 AP 的每个元素，递增***【CNT】***数组中元素的计数。返回计数最大的 ***cnt[]*** 数组的索引。
以下是上述方法的实施:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define MAXN 1000000

// Function to return element common
// in maximum number of APs
int maxCommonElement(int A[], int D[], int N)
{
    // Initialize the count variable
    int cnt[MAXN] = { 0 };

    for (int i = 0; i < N; i++) {

        // Increment count for every
        // element of an AP
        for (int j = A[i]; j < MAXN; j += D[i])
            cnt[j]++;
    }

    // Find the index with maximum count
    int com = max_element(cnt, cnt + MAXN) - cnt;

    // Return the maximum common element
    return com;
}

// Driver code
int main()
{
    int A[] = { 13, 1, 2, 5 },
        D[] = { 5, 10, 1, 12 };
    int N = sizeof(A) / sizeof(A[0]);

    cout << maxCommonElement(A, D, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    final static int MAXN = 1000000 ;

    static int max_element(int []A, int n)
    {
        int max = A[0];
        for(int i = 0; i < n; i++)
            if (A[i] > max )
                max = A[i];

        return max;
    }

    // Function to return element common
    // in maximum number of APs
    static int maxCommonElement(int A[], int D[], int N)
    {
        // Initialize the count variable
        int cnt[] = new int[MAXN] ;

        for (int i = 0; i < N; i++)
        {

            // Increment count for every
            // element of an AP
            for (int j = A[i]; j < MAXN; j += D[i])
                cnt[j]++;
        }

        // Find the index with maximum count
        int ans = 0;
        int com = 0;

        for(int i = 0; i < MAXN; i++)
        {
            if (cnt[i] > ans)
            {
                ans = cnt[i] ;
                com = i ;
            }
        }

        // Return the maximum common element
        return com;
    }

    // Driver code
    public static void main (String args[])
    {
        int A[] = { 13, 1, 2, 5 },
            D[] = { 5, 10, 1, 12 };

        int N = A.length;

        System.out.println(maxCommonElement(A, D, N));
    }
}

// This code is contributed by AnkitRai01
```

## 计算机编程语言

```
# Python implementation of the approach

MAXN = 1000000

# Function to return element common
# in maximum number of APs
def maxCommonElement(A, D, N):

    # Initialize the count variable
    cnt = [0] * MAXN

    for i in range(N):

        # Increment count for every
        # element of an AP
        for j in range(A[i], MAXN, D[i]):
            cnt[j] += 1

    # Find the index with maximum count
    ans = 0
    com = 0
    for i in range(MAXN):
        if cnt[i] > ans:
            ans = cnt[i]
            com = i

    # Return the maximum common element
    return com

# Driver code

A = [13, 1, 2, 5]
D = [5, 10, 1, 12]
N = len(A)

print(maxCommonElement(A, D, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    static int MAXN = 1000000 ;

    static int max_element(int []A, int n)
    {
        int max = A[0];
        for(int i = 0; i < n; i++)
            if (A[i] > max )
                max = A[i];

        return max;
    }

    // Function to return element common
    // in maximum number of APs
    static int maxCommonElement(int []A, int []D, int N)
    {
        // Initialize the count variable
        int []cnt = new int[MAXN] ;

        for (int i = 0; i < N; i++)
        {

            // Increment count for every
            // element of an AP
            for (int j = A[i]; j < MAXN; j += D[i])
                cnt[j]++;
        }

        // Find the index with maximum count
        int ans = 0;
        int com = 0;

        for(int i = 0; i < MAXN; i++)
        {
            if (cnt[i] > ans)
            {
                ans = cnt[i] ;
                com = i ;
            }
        }

        // Return the maximum common element
        return com;
    }

    // Driver code
    public static void Main ()
    {
        int []A = { 13, 1, 2, 5 };
        int []D = { 5, 10, 1, 12 };

        int N = A.Length;

        Console.WriteLine(maxCommonElement(A, D, N));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// Javascript implementation of the approach
var MAXN = 1000000;

// Function to return element common
// in maximum number of APs
function maxCommonElement(A, D, N)
{
    // Initialize the count variable
    var cnt = Array(MAXN).fill(0);

    for (var i = 0; i < N; i++) {

        // Increment count for every
        // element of an AP
        for (var j = A[i]; j < MAXN; j += D[i])
            cnt[j]++;
    }

    // Find the index with maximum count
    var ans = 0;
    var com = 0;

    for(var i = 0; i < MAXN; i++)
    {
        if (cnt[i] > ans)
        {
            ans = cnt[i] ;
            com = i ;
        }
    }

    // Return the maximum common element
    return com;
}

// Driver code
var A = [ 13, 1, 2, 5 ],
    D = [ 5, 10, 1, 12 ];
var N = A.length;
document.write( maxCommonElement(A, D, N));

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
41
```