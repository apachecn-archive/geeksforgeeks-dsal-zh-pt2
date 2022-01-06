# m 范围增量操作后数组中的最大值

> 原文:[https://www . geesforgeks . org/maximum-value-array-m-range-increment-operations/](https://www.geeksforgeeks.org/maximum-value-array-m-range-increment-operations/)

考虑一个大小为 n 的数组，所有初始值都为 0。我们需要执行以下 **m** 范围增量操作。

```
increment(a, b, k) : Increment values from 'a'
                     to 'b' by 'k'.    
```

在 m 次运算之后，我们需要计算数组中值的最大值。

**示例:**

```
Input : n = 5 m = 3
        a = 0, b = 1, k = 100
        a = 1, b = 4, k = 100
        a = 2, b = 3, k = 100
Output : 200
Explanation:
Initially array = {0, 0, 0, 0, 0}
After first operation:
array = {100, 100, 0, 0, 0}
After second operation:
array = {100, 200, 100, 100, 100}
After third operation:
array = {100, 200, 200, 200, 100}
Maximum element after m operations 
is 200.

Input : n = 4 m = 3
        a = 1, b = 2, k = 603
        a = 0, b = 0, k = 286
        a = 3, b = 3, k = 882
Output : 882
Explanation:
Initially array = {0, 0, 0, 0}
After first operation:
array = {0, 603, 603, 0}
After second operation:
array = {286, 603, 603, 0}
After third operation:
array = {286, 603, 603, 882}
Maximum element after m operations 
is 882.
```

一个**天真的方法**就是在给定的范围内进行每一个操作，然后最后找到最大数。

## C++

```
// C++ implementation of simple approach to
// find maximum value after m range increments.
#include<bits/stdc++.h>
using namespace std;

// Function to find the maximum element after
// m operations
int findMax(int n, int a[], int b[], int k[], int m)
{
    int arr[n];
    memset(arr, 0, sizeof(arr));

    // start performing m operations
    for (int i = 0; i< m; i++)
    {
        // Store lower and upper index i.e. range
        int lowerbound = a[i];
        int upperbound = b[i];

        // Add 'k[i]' value at this operation to
        // whole range
        for (int j=lowerbound; j<=upperbound; j++)
            arr[j] += k[i];
    }

    // Find maximum value after all operations and
    // return
    int res = INT_MIN;
    for (int i=0; i<n; i++)
        res = max(res, arr[i]);

    return res;
}

// Driver code
int main()
{
    // Number of values
    int n = 5;
    int a[] = {0, 1, 2};
    int b[] = {1, 4, 3};

    // value of k to be added at each operation
    int k[] = {100, 100, 100};

    int m = sizeof(a)/sizeof(a[0]);

    cout << "Maximum value after 'm' operations is "
        << findMax(n, a, b, k, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of simple approach
// to find maximum value after m range
// increments.
import java.util.*;

class GFG{

// Function to find the maximum element after
// m operations
static int findMax(int n, int a[],
                   int b[], int k[], int m)
{
    int[] arr = new int[n];

    // Start performing m operations
    for(int i = 0; i < m; i++)
    {

        // Store lower and upper index i.e. range
        int lowerbound = a[i];
        int upperbound = b[i];

        // Add 'k[i]' value at this operation to
        // whole range
        for(int j = lowerbound; j <= upperbound; j++)
            arr[j] += k[i];
    }

    // Find maximum value after all
    // operations and return
    int res = Integer.MIN_VALUE;
    for(int i = 0; i < n; i++)
        res = Math.max(res, arr[i]);

    return res;
}

// Driver Code
public static void main (String[] args)
{

    // Number of values
    int n = 5;
    int a[] = { 0, 1, 2 };
    int b[] = { 1, 4, 3 };

    // Value of k to be added at
    // each operation
    int k[] = { 100, 100, 100 };

    int m = a.length;

    System.out.println("Maximum value after 'm' " +
                       "operations is " +
                       findMax(n, a, b, k, m));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 progrma of
# simple approach to
# find maximum value
# after m range increments.
import sys

# Function to find the
# maximum element after
# m operations
def findMax(n, a, b, k, m):

  arr = [0] * n

  # Start performing m operations
  for i in range(m):

    # Store lower and upper
    # index i.e. range
    lowerbound = a[i]
    upperbound = b[i]

    # Add 'k[i]' value at
    # this operation to whole range
    for j in range (lowerbound,
                    upperbound + 1):
      arr[j] += k[i]

      # Find maximum value after
      # all operations and return
      res = -sys.maxsize - 1

      for i in range(n):
        res = max(res, arr[i])
        return res

# Driver code
if __name__ == "__main__":

  # Number of values
  n = 5
  a = [0, 1, 2]
  b = [1, 4, 3]

  # Value of k to be added
  # at each operation
  k = [100, 100, 100]

  m = len(a)

  print ("Maximum value after 'm' operations is ",
          findMax(n, a, b, k, m))

# This code is contributed by Chitranayal
```

## C#

```
// C# implementation of simple approach
// to find maximum value after m range
// increments.
using System;
public class GFG
{

  // Function to find the maximum element after
  // m operations
  static int findMax(int n, int[] a,
                     int[] b, int[] k, int m)
  {
    int[] arr = new int[n];

    // Start performing m operations
    for(int i = 0; i < m; i++)
    {

      // Store lower and upper index i.e. range
      int lowerbound = a[i];
      int upperbound = b[i];

      // Add 'k[i]' value at this operation to
      // whole range
      for(int j = lowerbound; j <= upperbound; j++)
        arr[j] += k[i];
    }

    // Find maximum value after all
    // operations and return
    int res = Int32.MinValue;
    for(int i = 0; i < n; i++)
      res = Math.Max(res, arr[i]);

    return res;
  }

  // Driver Code
  static public void Main ()
  {

    // Number of values
    int n = 5;
    int[] a = { 0, 1, 2 };
    int[] b = { 1, 4, 3 };

    // Value of k to be added at
    // each operation
    int[] k = { 100, 100, 100 };

    int m = a.Length;

    Console.WriteLine("Maximum value after 'm' " +
                      "operations is " +
                      findMax(n, a, b, k, m));
  }
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>
    // Javascript implementation of simple approach
    // to find maximum value after m range
    // increments.

    // Function to find the maximum element after
    // m operations
    function findMax(n, a, b, k, m)
    {
      let arr = new Array(n);
      arr.fill(0);

      // Start performing m operations
      for(let i = 0; i < m; i++)
      {

        // Store lower and upper index i.e. range
        let lowerbound = a[i];
        let upperbound = b[i];

        // Add 'k[i]' value at this operation to
        // whole range
        for(let j = lowerbound; j <= upperbound; j++)
          arr[j] += k[i];
      }

      // Find maximum value after all
      // operations and return
      let res = Number.MIN_VALUE;
      for(let i = 0; i < n; i++)
        res = Math.max(res, arr[i]);

      return res;
    }

    // Number of values
    let n = 5;
    let a = [ 0, 1, 2 ];
    let b = [ 1, 4, 3 ];

    // Value of k to be added at
    // each operation
    let k = [ 100, 100, 100 ];

    let m = a.length;

    document.write("Maximum value after 'm' " +
                      "operations is " +
                      findMax(n, a, b, k, m));

 // This code is contributed by rameshtravel07.
</script>
```

**输出:**

```
Maximum value after 'm' operations is 200
```

**时间复杂度:** O(m * max(范围))。这里，max(range)是指在一次操作中添加 k 的最大元素数。

**高效方法:**思路类似于[这个](https://www.geeksforgeeks.org/maximum-occurred-integer-n-ranges/)岗位。
在一次操作中执行两件事:
1-将 k 值添加到范围的唯一下限。
2-用 k 值减少上限+ 1 指数。
所有操作完成后，将所有值相加，检查最大和，打印最大和。

## C++

```
// C++ implementation of simple approach to
// find maximum value after m range increments.
#include<bits/stdc++.h>
using namespace std;

// Function to find maximum value after 'm' operations
int findMax(int n, int m, int a[], int b[], int k[])
{
    int arr[n+1];
    memset(arr, 0, sizeof(arr));

    // Start performing 'm' operations
    for (int i=0; i<m; i++)
    {
        // Store lower and upper index i.e. range
        int lowerbound = a[i];
        int upperbound = b[i];

        // Add k to the lower_bound
        arr[lowerbound] += k[i];

        // Reduce upper_bound+1 indexed value by k
        arr[upperbound+1] -= k[i];
    }

    // Find maximum sum possible from all values
    long long sum = 0, res = INT_MIN;
    for (int i=0; i < n; ++i)
    {
        sum += arr[i];
        res = max(res, sum);
    }

    // return maximum value
    return res;
}

// Driver code
int main()
{
    // Number of values
    int n = 5;

    int a[] = {0, 1, 2};
    int b[] = {1, 4, 3};
    int k[] = {100, 100, 100};

    // m is number of operations.
    int m = sizeof(a)/sizeof(a[0]);

    cout << "Maximum value after 'm' operations is "
         << findMax(n, m, a, b, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// simple approach to
// find maximum value after
// m range increments.
import java.io.*;

class GFG
{

// Function to find maximum
// value after 'm' operations
static long findMax(int n, int m,
                    int a[], int b[],
                    int k[])
{
    int []arr = new int[n + 1];
    //memset(arr, 0, sizeof(arr));

    // Start performing 'm' operations
    for (int i = 0; i < m; i++)
    {
        // Store lower and upper
        // index i.e. range
        int lowerbound = a[i];
        int upperbound = b[i];

        // Add k to the lower_bound
        arr[lowerbound] += k[i];

        // Reduce upper_bound+1
        // indexed value by k
        arr[upperbound + 1] -= k[i];
    }

    // Find maximum sum
    // possible from all values
    long sum = 0, res = Integer.MIN_VALUE;
    for (int i = 0; i < n; ++i)
    {
        sum += arr[i];
        res = Math.max(res, sum);
    }

    // return maximum value
    return res;
}

// Driver code
public static void main (String[] args)
{
    // Number of values
    int n = 5;

    int a[] = {0, 1, 2};
    int b[] = {1, 4, 3};
    int k[] = {100, 100, 100};

    // m is number of operations.
    int m = a.length;

    System.out.println("Maximum value after "+
                        "'m' operations is " +
                      findMax(n, m, a, b, k));
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Java implementation of
# simple approach to
# find maximum value after
#  m range increments.
import sys
def findMax(n, m, a, b, k):
    arr = [ 0 for i in range(n + 1)]

    for i in range(m):
        lowerbound = a[i]
        upperbound = b[i]

        arr[lowerbound] += k[i]
        arr[upperbound + 1] -= k[i]

    sum = 0
    res = -1-sys.maxsize

    for i in range(n):
        sum += arr[i]
        res = max(res, sum)
    return res

n = 5
a = [0, 1, 2]
b = [1, 4, 3]
k = [100, 100, 100]

m = len(a)

print("Maximum value after","'m' operations is", findMax(n, m, a, b, k))

# This code is contributed by rag2127
```

## C#

```
// c# implementation of
// simple approach to
// find maximum value after
// m range increments.
using System.Collections.Generic;
using System;
class GFG{

// Function to find maximum
// value after 'm' operations
static long findMax(int n, int m,
                    int []a, int []b,
                    int []k)
{
  int []arr = new int[n + 1];

  // Start performing 'm'
  // operations
  for (int i = 0; i < m; i++)
  {
    // Store lower and upper
    // index i.e. range
    int lowerbound = a[i];
    int upperbound = b[i];

    // Add k to the lower_bound
    arr[lowerbound] += k[i];

    // Reduce upper_bound+1
    // indexed value by k
    arr[upperbound + 1] -= k[i];
  }

  // Find maximum sum
  // possible from all values
  long sum = 0, res = -10000000;

  for (int i = 0; i < n; ++i)
  {
    sum += arr[i];
    res = Math.Max(res, sum);
  }

  // return maximum value
  return res;
}

// Driver code
public static void Main ()
{
  // Number of values
  int n = 5;

  int []a = {0, 1, 2};
  int []b = {1, 4, 3};
  int []k = {100, 100, 100};

  // m is number of operations.
  int m = a.Length;

  Console.WriteLine("Maximum value after " +
                    "'m' operations is " +
                     findMax(n, m, a, b, k));
}
}

// This code is contributed by Stream_Cipher
```

## java 描述语言

```
<script>
    // Javascript implementation of
    // simple approach to
    // find maximum value after
    // m range increments.

    // Function to find maximum
    // value after 'm' operations
    function findMax(n, m, a, b, k)
    {
      let arr = new Array(n + 1);
      arr.fill(0);

      // Start performing 'm'
      // operations
      for (let i = 0; i < m; i++)
      {
        // Store lower and upper
        // index i.e. range
        let lowerbound = a[i];
        let upperbound = b[i];

        // Add k to the lower_bound
        arr[lowerbound] += k[i];

        // Reduce upper_bound+1
        // indexed value by k
        arr[upperbound + 1] -= k[i];
      }

      // Find maximum sum
      // possible from all values
      let sum = 0, res = -10000000;

      for (let i = 0; i < n; ++i)
      {
        sum += arr[i];
        res = Math.max(res, sum);
      }

      // return maximum value
      return res;
    }

    // Number of values
    let n = 5;

    let a = [0, 1, 2];
    let b = [1, 4, 3];
    let k = [100, 100, 100];

    // m is number of operations.
    let m = a.length;

    document.write("Maximum value after " +
                      "'m' operations is " +
                       findMax(n, m, a, b, k));

</script>
```

**输出:**

```
Maximum value after 'm' operations is 200
```

**时间复杂度:** O(m + n)

本文由 [**萨哈布拉**](https://www.facebook.com/sahil.chhabra.965) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。