# 找到一个大小为 N 的数组，该数组正好有 K 个子数组，子数组的和为 S

> 原文:[https://www . geeksforgeeks . org/find-a-a-a-size-n-having-恰好 k-subarray-with-sum-s/](https://www.geeksforgeeks.org/find-an-array-of-size-n-having-exactly-k-subarrays-with-sum-s/)

给定三个整数 **N，K 和 S** ，任务是选择一个大小为 **N** 的数组，这样就正好存在具有和 **S** 的 **K** 子数组。
**注:**这个问题可以有很多解阵。
**举例:**

> **输入:** N = 4，K = 2，S = 3
> **输出:** 1 2 3 4
> **解释:**
> 其中一个可能的数组是【1，2，3，4】
> 正好存在两个和为 3 的子数组
> 和为(3)=[(1，2 ]，[ 3 ] ]
> **输入:** N = 5，K = 3， S = 50
> **输出:** 25 25 25 10 40
> **解释:**
> 其中一个可能的数组是【25，25，25，10，40】
> 正好存在三个求和为 50 的子数组
> 求和为(50)的子数组=[(25，25 ]，[ 25，25 ]，[ 10，40 ] ]

**方法:**
这个问题的一个解阵包含 **S** 元素 **K** 次和 **S+1** 元素 **(N-K)** 次，形成正好一个元素的 K 个子阵，S 为和。如果我们组合数组的任意两个或更多元素，那么它将给出大于 s 的和
下面是上述方法的实现:

## C++

```
// C++ program to find array
// with K subarrays with sum S

#include<bits/stdc++.h>
using namespace std;

// Function to find array
// with K subarrays with sum S
void SubarraysWithSumS(int n, int k, int s)
{
    for(int i=0;i<k;i++)
        cout << s << " ";
    for(int i=k;i<n;i++)
        cout << s+1 << " ";
}

// Driver Code
int main()
{
    int n = 4, k = 2, s = 3;

    // Function call
    SubarraysWithSumS(n, k, s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find array
// with K subarrays with sum S
class GFG
{

// Function to find array
// with K subarrays with sum S
static void SubarraysWithSumS(int n, int k, int s)
{
    for(int i = 0; i < k; i++)
        System.out.print(s + " ");
    for(int i = k; i < n; i++)
        System.out.print(s + 1 + " ");
}

// Driver Code
public static void main(String[] args)
{
    int n = 4, k = 2, s = 3;

    // Function call
    SubarraysWithSumS(n, k, s);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find array
# with K subarrays with sum S

# Function to find array
# with K subarrays with sum S
def SubarraysWithSumS(n, k, s):
    for i in range(k):
        print(s, end=" ")
    for i in range(k, n):
        print(s + 1, end = " ")

# Driver Code
n = 4
k = 2
s = 3

# Function call
SubarraysWithSumS(n, k, s)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find array
// with K subarrays with sum S
using System;

class GFG
{

// Function to find array
// with K subarrays with sum S
static void SubarraysWithSumS(int n, int k, int s)
{
    for(int i = 0; i < k; i++)
        Console.Write(s + " ");
    for(int i = k; i < n; i++)
        Console.Write(s + 1 + " ");
}

// Driver Code
public static void Main(String[] args)
{
    int n = 4, k = 2, s = 3;

    // Function call
    SubarraysWithSumS(n, k, s);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript program to find array
// with K subarrays with sum S

    // Function to find array
// with K subarrays with sum S
    function SubarraysWithSumS(n,k,s)
    {
        for(let i = 0; i < k; i++)
            document.write(s + " ");
    for(let i = k; i < n; i++)
        document.write(s + 1 + " ");
    }

    // Driver Code
    let n = 4, k = 2, s = 3;
    // Function call
    SubarraysWithSumS(n, k, s);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
3 3 4 4
```