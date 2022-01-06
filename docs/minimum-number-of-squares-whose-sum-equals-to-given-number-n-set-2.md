# 平方和等于给定数 N 的最小平方数|集合 2

> 原文:[https://www . geesforgeks . org/最小平方数-其和等于给定数-n-set-2/](https://www.geeksforgeeks.org/minimum-number-of-squares-whose-sum-equals-to-given-number-n-set-2/)

一个数总是可以表示为其他数的平方和。注意 1 是一个正方形，我们总是可以将一个数字破开为**(1 * 1+1 * 1+1 * 1+……)**。给定一个数字 **N** ，任务是将 **N** 表示为最小平方数之和。

**示例:**

> **输入:** 10
> **输出:** 1 + 9
> 这些都是可能的方式
> 1+1+1+1+1+1+1+1+1
> 1+1+1+1+1+4
> 1+1+4+4
> 1+9
> 选择一个数量最少的
> 
> **输入:**25
> T3】输出: 25

**先决条件:** [平方和等于给定数 N 的最小平方数](https://www.geeksforgeeks.org/minimum-number-of-squares-whose-sum-equals-to-given-number-n/)
**逼近:**这是[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)的典型应用。当我们从 N = 6 开始，减去 1 的平方，即 1 的 4 倍，再减去 2 的平方，即 4 的 1 倍，就可以得到 2。所以 2 的子问题被调用了两次。
由于相同的子问题被再次调用，所以这个问题具有重叠子问题的性质。So-min 平方和问题具有动态规划问题的两个性质(见[本](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)和[本](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/))。像其他典型的动态规划(DP)问题一样，通过自下而上的方式构造临时数组**表[][]** ，可以避免相同子问题的重新计算。
以下是上述方法的实施:

## C++

```
// C++ program to represent N as the
// sum of minimum square numbers.
#include <bits/stdc++.h>
using namespace std;

// Function for finding
// minimum square numbers
vector<int> minSqrNum(int n)
{
  // A[i] of array arr store
  // minimum count of
  // square number to get i
  int arr[n + 1], k;

  // sqrNum[i] store last
  // square number to get i
  int sqrNum[n + 1];
  vector<int> v;

  // Initialize
  arr[0] = 0;
  sqrNum[0] = 0;

  // Find minimum count of
  // square number for
  // all value 1 to n
  for (int i = 1; i <= n; i++)
  {
    // In worst case it will
    // be arr[i-1]+1 we use all
    // combination of a[i-1] and add 1
    arr[i] = arr[i - 1] + 1;
    sqrNum[i] = 1;

    k = 1;
    // Check for all square
    // number less or equal to i
    while (k * k <= i)
    {
      // if it gives less
      // count then update it
      if (arr[i] > arr[i - k * k] + 1)
      {
        arr[i] = arr[i - k * k] + 1;
        sqrNum[i] = k * k;
      }
      k++;
    }
  }

  // Vector v stores optimum
  // square number whose sum give N
  while (n > 0)
  {
    v.push_back(sqrNum[n]);
    n -= sqrNum[n];
  }
  return v;
}

// Driver code
int main()
{
  int n = 10;

  vector<int> v;

  // Calling function
  v = minSqrNum(n);

  // Printing vector
  for (auto i = v.begin();
            i != v.end(); i++)
  {
    cout << *i;
    if (i + 1 != v.end())
      cout << " + ";
  }
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to represent
// N as the sum of minimum
// square numbers.
import java.util.*;
class GFG{

// Function for finding
// minimum square numbers
static Vector<Integer> minSqrNum(int n)
{
  // A[i] of array arr store
  // minimum count of
  // square number to get i
  int []arr = new int[n + 1];
  int k = 0;

  // sqrNum[i] store last
  // square number to get i
  int []sqrNum = new int[n + 1];
  Vector<Integer> v = new Vector<>();

  // Initialize
  arr[0] = 0;
  sqrNum[0] = 0;

  // Find minimum count of
  // square number for
  // all value 1 to n
  for (int i = 1; i <= n; i++)
  {
    // In worst case it will
    // be arr[i-1]+1 we use all
    // combination of a[i-1] and add 1
    arr[i] = arr[i - 1] + 1;
    sqrNum[i] = 1;

    k = 1;
    // Check for all square
    // number less or equal to i
    while (k * k <= i)
    {
      // if it gives less
      // count then update it
      if (arr[i] > arr[i - k * k] + 1)
      {
        arr[i] = arr[i - k * k] + 1;
        sqrNum[i] = k * k;
      }
      k++;
    }
  }

  // Vector v stores optimum
  // square number whose sum give N
  while (n > 0)
  {
    v.add(sqrNum[n]);
    n -= sqrNum[n];
  }
  return v;
}

// Driver code
public static void main(String[] args)
{
  int n = 10;

  Vector<Integer> v;

  // Calling function
  v = minSqrNum(n);

  // Printing vector
  for (int i = 0; i <v.size(); i++)
  {
    System.out.print(v.elementAt(i));
    if (i+1 != v.size())
      System.out.print(" + ");
  }
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program to represent N as the
# sum of minimum square numbers.

# Function for finding
# minimum square numbers
def minSqrNum(n):

    # arr[i] of array arr store
    # minimum count of
    # square number to get i
    arr = [0] * (n + 1)

    # sqrNum[i] store last
    # square number to get i
    sqrNum = [0] * (n + 1)
    v = []

    # Find minimum count of
    # square number for
    # all value 1 to n
    for i in range(n + 1):

        # In worst case it will
        # be arr[i-1]+1 we use all
        # combination of a[i-1] and add 1
        arr[i] = arr[i - 1] + 1
        sqrNum[i] = 1

        k = 1;

        # Check for all square
        # number less or equal to i
        while (k * k <= i):

            # If it gives less
            # count then update it
            if (arr[i] > arr[i - k * k] + 1):
                arr[i] = arr[i - k * k] + 1
                sqrNum[i] = k * k

            k += 1

    # v stores optimum
    # square number whose sum give N
    while (n > 0):
        v.append(sqrNum[n])
        n -= sqrNum[n];

    return v

# Driver code
n = 10

# Calling function
v = minSqrNum(n)

# Printing vector
for i in range(len(v)):
    print(v[i], end = "")

    if (i < len(v) - 1):
        print(" + ", end = "")

# This article is contributed by Apurvaraj
```

## C#

```
// C# program to represent
// N as the sum of minimum
// square numbers.
using System;
using System.Collections.Generic;
class GFG{

// Function for finding
// minimum square numbers
static List<int> minSqrNum(int n)
{
  // A[i] of array arr store
  // minimum count of
  // square number to get i
  int []arr = new int[n + 1];
  int k = 0;

  // sqrNum[i] store last
  // square number to get i
  int []sqrNum = new int[n + 1];
  List<int> v = new List<int>();

  // Initialize
  arr[0] = 0;
  sqrNum[0] = 0;

  // Find minimum count of
  // square number for
  // all value 1 to n
  for (int i = 1; i <= n; i++)
  {
    // In worst case it will
    // be arr[i-1]+1 we use all
    // combination of a[i-1] and add 1
    arr[i] = arr[i - 1] + 1;
    sqrNum[i] = 1;

    k = 1;
    // Check for all square
    // number less or equal to i
    while (k * k <= i)
    {
      // if it gives less
      // count then update it
      if (arr[i] > arr[i - k * k] + 1)
      {
        arr[i] = arr[i - k * k] + 1;
        sqrNum[i] = k * k;
      }
      k++;
    }
  }

  // List v stores optimum
  // square number whose sum give N
  while (n > 0)
  {
    v.Add(sqrNum[n]);
    n -= sqrNum[n];
  }
  return v;
}

// Driver code
public static void Main(String[] args)
{
  int n = 10;

  List<int> v;

  // Calling function
  v = minSqrNum(n);

  // Printing vector
  for (int i = 0; i <v.Count; i++)
  {
    Console.Write(v[i]);
    if (i+1 != v.Count)
      Console.Write(" + ");
  }
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript program to represent N as the
// sum of minimum square numbers.

// Function for finding
// minimum square numbers
function minSqrNum(n)
{
  // A[i] of array arr store
  // minimum count of
  // square number to get i
  var arr = Array(n+1), k;

  // sqrNum[i] store last
  // square number to get i
  var sqrNum = Array(n+1);
  var v = [];

  // Initialize
  arr[0] = 0;
  sqrNum[0] = 0;

  // Find minimum count of
  // square number for
  // all value 1 to n
  for (var i = 1; i <= n; i++)
  {
    // In worst case it will
    // be arr[i-1]+1 we use all
    // combination of a[i-1] and add 1
    arr[i] = arr[i - 1] + 1;
    sqrNum[i] = 1;

    k = 1;
    // Check for all square
    // number less or equal to i
    while (k * k <= i)
    {
      // if it gives less
      // count then update it
      if (arr[i] > arr[i - k * k] + 1)
      {
        arr[i] = arr[i - k * k] + 1;
        sqrNum[i] = k * k;
      }
      k++;
    }
  }

  // Vector v stores optimum
  // square number whose sum give N
  while (n > 0)
  {
    v.push(sqrNum[n]);
    n -= sqrNum[n];
  }
  return v;
}

// Driver code
var n = 10;
var v = [];
// Calling function
v = minSqrNum(n);
// Printing vector
for(var i = 0; i<v.length; i++)
{
    document.write(v[i]);
  if (i + 1 != v.length)
    document.write( " + ");
}

</script>
```

**Output:** 

```
1 + 9
```

时间复杂度:O(n <sup>3/2</sup> )

辅助空间:O(n)