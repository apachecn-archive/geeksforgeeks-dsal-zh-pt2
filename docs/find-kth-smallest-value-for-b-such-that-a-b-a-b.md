# 求 b 的第 k 个最小值，使得 a + b = a | b

> 原文:[https://www . geesforgeks . org/find-kth-mini-value-for-b-so-a-b-a-b/](https://www.geeksforgeeks.org/find-kth-smallest-value-for-b-such-that-a-b-a-b/)

给定数字 **a** 和 **k** ，任务是为 **b** 找到**第 k 个**最小值，使得 **a + b = a | b** ，其中“|”表示 [**按位 OR**](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/) 运算符。a 和 k 的最大值可以是![10^9](img/3d20ee38faaaf17725a876a5dd338390.png "Rendered by QuickLaTeX.com")。

**示例:**

```
Input: a = 10, k = 3
Output: 5
Numbers satisfying the condition 5 + b = 5 | b
are 1, 4, 5, etc.
Since 3rd smallest value for b is required,
hence b = 5.

Input: a = 1, k = 1
Output: 2
Numbers satisfying the condition 1 + b = 1 | b
are 2, 4, 6, etc.
Since 1st smallest value for b is required,
hence b = 2.
```

**进场:**

*   b 是给定方程**的解当且仅当 b 在所有位置都为 0，其中 a 为 1(以二进制表示)**。
*   因此，我们需要确定位置 a 为 0 时的 b 位。假设 **a = 10100001** 那么 b 的最后八位数字一定是 **b = 0*0****0** ，其中‘*’表示 0 或 1。**将所有“*”替换为 0 或 1** 就能解决问题。
*   第 k 个最小的数字将通过**用数字 k** 的二进制表示的数字替换 y 中的所有' * '来接收。
*   由于 a 和 k 的最大值是![10^9](img/3d20ee38faaaf17725a876a5dd338390.png "Rendered by QuickLaTeX.com")，所以检查二进制表示中的 **32 个位置**就足以得到给定方程的正确答案。

下面是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find k'th smallest value for b
// such that a + b = a | b

#include <bits/stdc++.h>
using namespace std;

#define ll long long

// Function to find
// the kth smallest value for b
ll kthSmallest(ll a, ll k)
{

    // res will store final answer
    ll res = 0;
    ll j = 0;
    for (ll i = 0; i < 32; i++) {

        // skip when j'th position
        // has 1 in binary representation
        // as in res, j'th position will be 0.

        while (j < 32 && (a & (1 << j)))
            // j'th bit is set
            j++;

        // if i'th bit of k is 1
        // and i'th bit of j is 0
        // then set i'th bit in res.

        if (k & (1 << i)) // i'th bit is set
            res |= (1LL << j);

        // proceed to next bit
        j++;
    }
    return res;
}

// Driver Code
int main()
{

    ll a = 10, k = 3;

    cout << kthSmallest(a, k) << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find k'th smallest value for b
// such that a + b = a | b
class GFG
{

    // Function to find
    // the kth smallest value for b
    static int kthSmallest(int a, int k)
    {

        // res wiint store final answer
        int res = 0;
        int j = 0;
        for (int i = 0; i < 32; i++)
        {

            // skip when j'th position
            // has 1 in binary representation
            // as in res, j'th position wiint be 0.
            while (j < 32 && (a & (1 << j)) > 0)

                // j'th bit is set
                j++;

            // if i'th bit of k is 1
            // and i'th bit of j is 0
            // then set i'th bit in res.
            if ((k & (1 << i)) > 0) // i'th bit is set
                res |= (1 << j);

            // proceed to next bit
            j++;
        }
        return res;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int a = 10, k = 3;

        System.out.print(kthSmallest(a, k) + "\n");
    }
}

// This code is contributed by Rajput-Ji
```

## 计算机编程语言

```
# Python3 program to find k'th smallest value for b
# such that a + b = a | b

# Function to find
# the kth smallest value for b
def kthSmallest(a, k):

    # res wistore final answer
    res = 0
    j = 0
    for i in range(32):

        # skip when j'th position
        # has 1 in binary representation
        # as in res, j'th position wibe 0.
        while (j < 32 and (a & (1 << j))):

            # j'th bit is set
            j += 1

        # if i'th bit of k is 1
        # and i'th bit of j is 0
        # then set i'th bit in res.

        if (k & (1 << i)): # i'th bit is set
            res |= (1 << j)

        # proceed to next bit
        j += 1
    return res

# Driver Code

a = 10
k = 3

print(kthSmallest(a, k))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find k'th smallest value for b
// such that a + b = a | b
using System;

class GFG
{

    // Function to find
    // the kth smallest value for b
    static int kthSmallest(int a, int k)
    {

        // res wiint store final answer
        int res = 0;
        int j = 0;
        for (int i = 0; i < 32; i++)
        {

            // skip when j'th position
            // has 1 in binary representation
            // as in res, j'th position wiint be 0.
            while (j < 32 && (a & (1 << j)) > 0)

                // j'th bit is set
                j++;

            // if i'th bit of k is 1
            // and i'th bit of j is 0
            // then set i'th bit in res.
            if ((k & (1 << i)) > 0) // i'th bit is set
                res |= (1 << j);

            // proceed to next bit
            j++;
        }
        return res;
    }

    // Driver Code
    public static void Main()
    {
        int a = 10, k = 3;

        Console.WriteLine(kthSmallest(a, k));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript program to find k'th smallest value for b
// such that a + b = a | b

// Function to find
// the kth smallest value for b
function kthSmallest(a, k)
{

    // res will store final answer
    var res = 0;
    var j = 0;
    for (var i = 0; i < 32; i++) {

        // skip when j'th position
        // has 1 in binary representation
        // as in res, j'th position will be 0.

        while (j < 32 && (a & (1 << j)))
            // j'th bit is set
            j++;

        // if i'th bit of k is 1
        // and i'th bit of j is 0
        // then set i'th bit in res.

        if (k & (1 << i)) // i'th bit is set
            res |= (1 << j);

        // proceed to next bit
        j++;
    }
    return res;
}

// Driver Code
var a = 10, k = 3;
document.write( kthSmallest(a, k));

</script>
```

**Output:** 

```
5
```

**时间复杂度:** O(N)