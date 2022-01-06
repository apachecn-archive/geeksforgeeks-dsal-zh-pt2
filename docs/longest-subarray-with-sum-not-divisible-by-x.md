# 总和不能被 X 整除的最长子阵列

> 原文:[https://www . geeksforgeeks . org/sum 不能被 x 整除的最长子数组/](https://www.geeksforgeeks.org/longest-subarray-with-sum-not-divisible-by-x/)

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和一个整数 **X** ，任务是打印[最长的子数组，这样它的元素之和就不能被 **X**](https://www.geeksforgeeks.org/count-of-longest-possible-subarrays-with-sum-not-divisible-by-k/) 整除。如果没有这样的子阵列，打印【T10 "-" 1 "。
**注意:**如果给定属性存在多个子阵列，打印其中任意一个。
**举例:**

> **输入:** arr[] = {1，2，3} X = 3
> **输出:** 2 3
> **解释:**
> 子阵列{2，3}有一个元素之和 **5** ，不能被 **3** 整除。
> **输入:** arr[] = {2，6} X = 2
> **输出:** -1
> **解释:**
> 所有可能的子阵{1}、{2}、{1，2}都有一个偶和。
> 所以，答案是-1。

**天真法:**解决问题最简单的方法就是[生成所有可能的子阵](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)并不断计算其和。如果发现任何子阵列的和不能被 **X** 整除，将长度与获得的最大长度( **maxm** )进行比较，并相应更新 **maxm** ，并更新子阵列的**起始索引**和**结束索引**。最后，打印具有存储的开始和结束索引的子阵列。如果没有这样的子阵列，则打印**-1”**。
**时间复杂度:***O(N<sup>2</sup>)*
**辅助空间:** *O(1)*

**高效方法:**为了优化上述方法，我们将找到[前缀和后缀数组之和](https://www.geeksforgeeks.org/index-with-minimum-sum-of-prefix-and-suffix-sums-in-an-array/)。请遵循以下步骤:

*   生成 [**前缀和数组**](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/) 和**后缀和数组**。
*   使用[两个指针](https://www.geeksforgeeks.org/two-pointers-technique/)从**【0，N–1】**迭代，选择每个索引处不能被 **X** 整除的元素的前缀和后缀之和。存储子阵列的**起始索引和**结束索引。
*   完成上述步骤后，如果存在总和不能被 **X** 整除的子阵列，则打印具有存储的**开始和结束索引**的子阵列。
*   如果没有这样的子阵列，则打印**-1”**。

下面是上述方法的实现:

## C++

```
#include <iostream>
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the longest
// subarray with sum of elements
// not divisible by X
void max_length(int N, int x,
                vector<int>& v)
{
    int i, a;

    // Pref[] stores the prefix sum
    // Suff[] stores the suffix sum
    vector<int> preff, suff;
    int ct = 0;

    for (i = 0; i < N; i++) {

        a = v[i];

        // If array element is
        // divisibile by x
        if (a % x == 0) {

            // Increase count
            ct += 1;
        }
    }

    // If all the array elements
    // are divisible by x
    if (ct == N) {

        // No subarray possible
        cout << -1 << endl;
        return;
    }

    // Reverse v to calculate the
    // suffix sum
    reverse(v.begin(), v.end());

    suff.push_back(v[0]);

    // Calculate the suffix sum
    for (i = 1; i < N; i++) {
        suff.push_back(v[i]
                       + suff[i - 1]);
    }

    // Reverse to original form
    reverse(v.begin(), v.end());

    // Reverse the suffix sum array
    reverse(suff.begin(), suff.end());

    preff.push_back(v[0]);

    // Calculate the prefix sum
    for (i = 1; i < N; i++) {
        preff.push_back(v[i]
                        + preff[i - 1]);
    }

    int ans = 0;

    // Stores the starting index
    // of required subarray
    int lp = 0;

    // Stores the ending index
    // of required subarray
    int rp = N - 1;

    for (i = 0; i < N; i++) {

        // If suffix sum till i-th
        // index is not divisible by x
        if (suff[i] % x != 0
            && (ans < (N - 1))) {

            lp = i;
            rp = N - 1;

            // Update the answer
            ans = max(ans, N - i);
        }

        // If prefix sum till i-th
        // index is not divisible by x
        if (preff[i] % x != 0
            && (ans < (i + 1))) {

            lp = 0;
            rp = i;

            // Update the answer
            ans = max(ans, i + 1);
        }
    }

    // Print the longest subarray
    for (i = lp; i <= rp; i++) {
        cout << v[i] << " ";
    }
}

// Driver Code
int main()
{
    int x = 3;

    vector<int> v = { 1, 3, 2, 6 };
    int N = v.size();

    max_length(N, x, v);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to print the longest
// subarray with sum of elements
// not divisible by X
static void max_length(int N, int x,
                       int []v)
{
    int i, a;

    // Pref[] stores the prefix sum
    // Suff[] stores the suffix sum
    List<Integer> preff = new Vector<Integer>();
    List<Integer> suff = new Vector<Integer>();

    int ct = 0;

    for(i = 0; i < N; i++) 
    {
        a = v[i];

        // If array element is
        // divisibile by x
        if (a % x == 0)
        {

            // Increase count
            ct += 1;
        }
    }

    // If all the array elements
    // are divisible by x
    if (ct == N) 
    {

        // No subarray possible
        System.out.print(-1 + "\n");
        return;
    }

    // Reverse v to calculate the
    // suffix sum
    v = reverse(v);

    suff.add(v[0]);

    // Calculate the suffix sum
    for(i = 1; i < N; i++)
    {
        suff.add(v[i] + suff.get(i - 1));
    }

    // Reverse to original form
    v = reverse(v);

    // Reverse the suffix sum array
    Collections.reverse(suff);

    preff.add(v[0]);

    // Calculate the prefix sum
    for(i = 1; i < N; i++)
    {
        preff.add(v[i] + preff.get(i - 1));
    }

    int ans = 0;

    // Stores the starting index
    // of required subarray
    int lp = 0;

    // Stores the ending index
    // of required subarray
    int rp = N - 1;

    for(i = 0; i < N; i++)
    {

        // If suffix sum till i-th
        // index is not divisible by x
        if (suff.get(i) % x != 0 &&
           (ans < (N - 1))) 
        {
            lp = i;
            rp = N - 1;

            // Update the answer
            ans = Math.max(ans, N - i);
        }

        // If prefix sum till i-th
        // index is not divisible by x
        if (preff.get(i) % x != 0 &&
           (ans < (i + 1)))
        {
            lp = 0;
            rp = i;

            // Update the answer
            ans = Math.max(ans, i + 1);
        }
    }

    // Print the longest subarray
    for(i = lp; i <= rp; i++)
    {
        System.out.print(v[i] + " ");
    }
}

static int[] reverse(int a[]) 
{
    int i, n = a.length, t;
    for(i = 0; i < n / 2; i++)
    {
        t = a[i];
        a[i] = a[n - i - 1];
        a[n - i - 1] = t;
    }
    return a;
}

// Driver Code
public static void main(String[] args)
{
    int x = 3;
    int []v = { 1, 3, 2, 6 };
    int N = v.length;

    max_length(N, x, v);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to implement 
# the above approach 

# Function to print the longest 
# subarray with sum of elements 
# not divisible by X 
def max_length(N, x, v):

    # Pref[] stores the prefix sum 
    # Suff[] stores the suffix sum 
    preff, suff = [], []
    ct = 0

    for i in range(N):
        a = v[i]

        # If array element is 
        # divisibile by x 
        if a % x == 0:

            # Increase count 
            ct += 1

    # If all the array elements 
    # are divisible by x 
    if ct == N:

        # No subarray possible 
        print(-1)
        return

    # Reverse v to calculate the 
    # suffix sum 
    v.reverse()

    suff.append(v[0])

    # Calculate the suffix sum 
    for i in range(1, N):
        suff.append(v[i] + suff[i - 1])

    # Reverse to original form 
    v.reverse()

    # Reverse the suffix sum array
    suff.reverse()

    preff.append(v[0])

    # Calculate the prefix sum
    for i in range(1, N):
        preff.append(v[i] + preff[i - 1])

    ans = 0

    # Stores the starting index 
    # of required subarray 
    lp = 0

    # Stores the ending index 
    # of required subarray 
    rp = N - 1

    for i in range(N):

        # If suffix sum till i-th 
        # index is not divisible by x 
        if suff[i] % x != 0 and ans < N - 1:
            lp = i
            rp = N - 1

            # Update the answer
            ans = max(ans, N - i)

        # If prefix sum till i-th 
        # index is not divisible by x 
        if preff[i] % x != 0 and ans < i + 1:
            lp = 0
            rp = i

            # Update the answer
            ans = max(ans, i + 1)

    # Print the longest subarray
    for i in range(lp, rp + 1):
        print(v[i], end = " ")

# Driver code
x = 3
v = [ 1, 3, 2, 6 ]
N = len(v)

max_length(N, x, v)

# This code is contributed by Stuti Pathak
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to print the longest
// subarray with sum of elements
// not divisible by X
static void max_length(int N, int x,
                       int []v)
{
    int i, a;

    // Pref[] stores the prefix sum
    // Suff[] stores the suffix sum
    List<int> preff = new List<int>();
    List<int> suff = new List<int>();

    int ct = 0;

    for(i = 0; i < N; i++) 
    {
        a = v[i];

        // If array element is
        // divisibile by x
        if (a % x == 0)
        {

            // Increase count
            ct += 1;
        }
    }

    // If all the array elements
    // are divisible by x
    if (ct == N) 
    {

        // No subarray possible
        Console.Write(-1 + "\n");
        return;
    }

    // Reverse v to calculate the
    // suffix sum
    v = reverse(v);

    suff.Add(v[0]);

    // Calculate the suffix sum
    for(i = 1; i < N; i++)
    {
        suff.Add(v[i] + suff[i - 1]);
    }

    // Reverse to original form
    v = reverse(v);

    // Reverse the suffix sum array
    suff.Reverse();

    preff.Add(v[0]);

    // Calculate the prefix sum
    for(i = 1; i < N; i++)
    {
        preff.Add(v[i] + preff[i - 1]);
    }

    int ans = 0;

    // Stores the starting index
    // of required subarray
    int lp = 0;

    // Stores the ending index
    // of required subarray
    int rp = N - 1;

    for(i = 0; i < N; i++)
    {

        // If suffix sum till i-th
        // index is not divisible by x
        if (suff[i] % x != 0 &&
               (ans < (N - 1))) 
        {
            lp = i;
            rp = N - 1;

            // Update the answer
            ans = Math.Max(ans, N - i);
        }

        // If prefix sum till i-th
        // index is not divisible by x
        if (preff[i] % x != 0 &&
                (ans < (i + 1)))
        {
            lp = 0;
            rp = i;

            // Update the answer
            ans = Math.Max(ans, i + 1);
        }
    }

    // Print the longest subarray
    for(i = lp; i <= rp; i++)
    {
        Console.Write(v[i] + " ");
    }
}

static int[] reverse(int []a) 
{
    int i, n = a.Length, t;
    for(i = 0; i < n / 2; i++)
    {
        t = a[i];
        a[i] = a[n - i - 1];
        a[n - i - 1] = t;
    }
    return a;
}

// Driver Code
public static void Main(String[] args)
{
    int x = 3;
    int []v = { 1, 3, 2, 6 };
    int N = v.Length;

    max_length(N, x, v);
}
}

// This code is contributed by PrinciRaj1992
```

**Output:** 

```
3 2 6

```

**时间复杂度:***O(N)*
T5】辅助空间: *O(N)*