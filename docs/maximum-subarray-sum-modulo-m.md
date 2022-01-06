# 最大子阵列和模 m

> 原文:[https://www . geesforgeks . org/maximum-subarray-sum-modal-m/](https://www.geeksforgeeks.org/maximum-subarray-sum-modulo-m/)

给定一个由 **n 个**元素和一个整数 m 组成的数组，任务是找到它的子阵列模 m 之和的最大值，即找到每个子阵列模 m 之和，并打印这个模运算的最大值。
**例:**

```
Input : arr[] = { 3, 3, 9, 9, 5 }
        m = 7
Output : 6
All sub-arrays and their value:
{ 9 } => 9%7 = 2
{ 3 } => 3%7 = 3
{ 5 } => 5%7 = 5
{ 9, 5 } => 14%7 = 2
{ 9, 9 } => 18%7 = 4
{ 3, 9 } => 12%7 = 5
{ 3, 3 } => 6%7 = 6
{ 3, 9, 9 } => 21%7 = 0
{ 3, 3, 9 } => 15%7 = 1
{ 9, 9, 5 } => 23%7 = 2
{ 3, 3, 9, 9 } => 24%7 = 3
{ 3, 9, 9, 5 } => 26%7 = 5
{ 3, 3, 9, 9, 5 } => 29%7 = 1

Input : arr[] = {10, 7, 18}
        m = 13
Output : 12
The subarray {7, 18} has maximum sub-array
sum modulo 13.
```

**方法 1(蛮力):**
使用蛮力找到给定阵列的所有子阵列，并找到每个子阵列 mod m 的和，并跟踪最大值。
**方法二(高效途径):**
思路是计算数组的前缀和。我们找到以每个索引结尾的最大和，并最终返回总体最大值。要找到以指数结尾的最大和，我们需要找到以 I 结尾的最大和的起点。下面的步骤解释了如何找到起点。

```
Let prefix sum for index i be prefixi, i.e., 
prefixi = (arr[0] + arr[1] + .... arr[i] ) % m

Let maximum sum ending with i be, maxSumi. 
Let this sum begins with index j.

maxSumi = (prefixi - prefixj + m) % m

From above expression it is clear that the
value of maxSumi becomes maximum when 
prefixj is greater than prefixi 
and closest to prefixi
```

在上面的算法中，我们主要有两个操作。

1.  存储所有前缀。
2.  对于当前前缀，前缀 <sub>i</sub> ，找到大于等于前缀 <sub>i</sub> + 1 的最小值。

对于上面的操作，像 AVL 树、红黑树等自平衡二进制搜索树是最适合的。在下面的实现中，我们使用 STL 中的[集，它实现了一个自平衡二进制搜索树。
以下是本办法的实施情况:](https://www.geeksforgeeks.org/set-in-cpp-stl/) 

## C++

```
// C++ program to find sub-array having maximum
// sum of elements modulo m.
#include<bits/stdc++.h>
using namespace std;

// Return the maximum sum subarray mod m.
int maxSubarray(int arr[], int n, int m)
{
    int x, prefix = 0, maxim = 0;

    set<int> S;
    S.insert(0);   

    // Traversing the array.
    for (int i = 0; i < n; i++)
    {
        // Finding prefix sum.
        prefix = (prefix + arr[i])%m;

        // Finding maximum of prefix sum.
        maxim = max(maxim, prefix);

        // Finding iterator pointing to the first
        // element that is not less than value
        // "prefix + 1", i.e., greater than or
        // equal to this value.
        auto it = S.lower_bound(prefix+1);

        if (it != S.end())
            maxim = max(maxim, prefix - (*it) + m );

        // Inserting prefix in the set.
        S.insert(prefix);
    }

    return maxim;
}

// Driver Program
int main()
{
    int arr[] = { 3, 3, 9, 9, 5 };
    int n = sizeof(arr)/sizeof(arr[0]);
    int m = 7;
    cout << maxSubarray(arr, n, m) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sub-array
// having maximum sum of elements modulo m.
import java.util.*;
class GFG
{

  // Return the maximum sum subarray mod m.
  static int maxSubarray(int[] arr, int n, int m)
  {
    int x = 0;
    int prefix = 0;
    int maxim = 0;
    Set<Integer> S = new HashSet<Integer>();
    S.add(0);

    // Traversing the array.
    for (int i = 0; i < n; i++)
    {

      // Finding prefix sum.
      prefix = (prefix + arr[i]) % m;

      // Finding maximum of prefix sum.
      maxim = Math.max(maxim, prefix);

      // Finding iterator poing to the first
      // element that is not less than value
      // "prefix + 1", i.e., greater than or
      // equal to this value.
      int it = 0;

      for (int j : S)
      {
        if (j >= prefix + 1)
          it = j;
      }
      if (it != 0)
      {
        maxim = Math.max(maxim, prefix - it + m);
      }

      // adding prefix in the set.
      S.add(prefix);
    }
    return maxim;
  }

  // Driver code
  public static void main(String[] args)
  {

    // Driver Code
    int[] arr = new int[] { 3, 3, 9, 9, 5 };
    int n = 5;
    int m = 7;
    System.out.print(maxSubarray(arr, n, m));
  }
}

// This code is contributed by pratham76.
```

## 蟒蛇 3

```
# Python3 program to find sub-array
# having maximum sum of elements modulo m.

# Return the maximum sum subarray mod m.
def maxSubarray(arr, n, m):

    x = 0
    prefix = 0
    maxim = 0

    S = set()
    S.add(0)    

    # Traversing the array.
    for i in range(n):

        # Finding prefix sum.
        prefix = (prefix + arr[i]) % m

        # Finding maximum of prefix sum.
        maxim = max(maxim, prefix)

        # Finding iterator poing to the first
        # element that is not less than value
        # "prefix + 1", i.e., greater than or
        # equal to this value.
        it = 0
        for i in S:
            if i >= prefix + 1:
                it = i
        if (it != 0) :
                maxim = max(maxim, prefix - it + m )

        # adding prefix in the set.
        S.add(prefix)

    return maxim

# Driver Code
arr = [3, 3, 9, 9, 5]
n = 5
m = 7
print(maxSubarray(arr, n, m))

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# program to find sub-array
// having maximum sum of elements modulo m.
using System;
using System.Collections;
using System.Collections.Generic;

class GFG
{

  // Return the maximum sum subarray mod m.
  static int maxSubarray(int[] arr, int n, int m)
  {

    int prefix = 0;
    int maxim = 0;
    HashSet<int> S = new HashSet<int>();
    S.Add(0);

    // Traversing the array.
    for (int i = 0; i < n; i++)
    {

      // Finding prefix sum.
      prefix = (prefix + arr[i]) % m;

      // Finding maximum of prefix sum.
      maxim = Math.Max(maxim, prefix);

      // Finding iterator poing to the first
      // element that is not less than value
      // "prefix + 1", i.e., greater than or
      // equal to this value.
      int it = 0;

      foreach(int j in S)
      {
        if (j >= prefix + 1)
          it = j;
      }
      if (it != 0)
      {
        maxim = Math.Max(maxim, prefix - it + m);
      }

      // adding prefix in the set.
      S.Add(prefix);
    }
    return maxim;
  }

  // Driver code
  public static void Main(string[] args)
  {

    int[] arr = new int[] { 3, 3, 9, 9, 5 };
    int n = 5;
    int m = 7;
    Console.Write(maxSubarray(arr, n, m));
  }
}

// This code is contributed by rutvik_56.
```

## java 描述语言

```
<script>
// Javascript program to find sub-array
// having maximum sum of elements modulo m.

// Return the maximum sum subarray mod m.
function maxSubarray(arr,n,m)
{
    let x = 0;
    let prefix = 0;
    let maxim = 0;
    let S = new Set();
    S.add(0);

    // Traversing the array.
    for (let i = 0; i < n; i++)
    {

      // Finding prefix sum.
      prefix = (prefix + arr[i]) % m;

      // Finding maximum of prefix sum.
      maxim = Math.max(maxim, prefix);

      // Finding iterator poing to the first
      // element that is not less than value
      // "prefix + 1", i.e., greater than or
      // equal to this value.
      let it = 0;

      for (let j of S.values())
      {
        if (j >= prefix + 1)
          it = j;
      }
      if (it != 0)
      {
        maxim = Math.max(maxim, prefix - it + m);
      }

      // adding prefix in the set.
      S.add(prefix);
    }
    return maxim;
}

 // Driver Code
let arr=[3, 3, 9, 9, 5];
let n = 5;
let m = 7;
document.write(maxSubarray(arr, n, m));

// This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
6
```

**参考:**
[http://stackoverflow . com/questions/31113993/maximum-subarray-sum-module-m](http://stackoverflow.com/questions/31113993/maximum-subarray-sum-modulo-m)
本文由 **Anuj Chauhan** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。