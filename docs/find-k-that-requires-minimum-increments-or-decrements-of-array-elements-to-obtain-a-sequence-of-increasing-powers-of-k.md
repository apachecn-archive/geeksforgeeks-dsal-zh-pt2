# 找到需要最小数组元素增量或减量的 K，以获得 K 的递增幂序列

> 原文:[https://www . geeksforgeeks . org/find-k-需要数组元素的最小递增或递减来获得 k 的递增幂序列/](https://www.geeksforgeeks.org/find-k-that-requires-minimum-increments-or-decrements-of-array-elements-to-obtain-a-sequence-of-increasing-powers-of-k/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)，任务是找到需要最小移动次数的整数 **K** ，将给定数组转换为 K 的幂序列，即 **{K <sup>0</sup> ，K <sup>1</sup> ，K <sup>2</sup> ，…。，K<sup>N–1</sup>}**。在每次移动中，增加或减少一个数组元素。

**示例:**

> **输入:** arr[] = {1，2，3}
> **输出:** 2
> **解释:**通过将 arr[2]递增 1，修改为{1，2，4}，等于{2 <sup>0</sup> ，2 <sup>1</sup> ，2 <sup>2</sup> }。因此，K = 2。
> 
> **输入:** arr[] = {1，9，27}
> **输出:** 5
> **说明:**将阵法修改为{1，5，25}需要的移动次数最少。因此，K = 5。

**方法:**思路是从 **1** 开始检查所有的数字，直到一个数字的幂越过**最大值，即 10 <sup>10</sup>** (假设)。按照以下步骤解决问题:

1.  检查从 **1** 到 **x** 的所有数字，直到**x<sup>N–1</sup><数组的 max _ element****+1****移动的值需要转换为 1** 的幂。
2.  用该元素的幂来计算数组所需的移动次数。
3.  如果所需的移动小于前一个值，则更新 **K** 和 **min moves** 的值。
4.  打印 **K** 的值。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

#define ll long long

// Function to find the value of K such
// that it takes minimum number of moves
// to convert the array in its power
ll findMinCostInteger(vector<ll>& a)
{

    // Size of the array
    int n = a.size();

    // Finding tha sum of the array
    ll sum = accumulate(a.begin(),
                        a.end(), 0);

    ll K = 0, minmove = LLONG_MAX;

    // Find K for which the count
    // of moves will become minimum
    for (int i = 1;; ++i) {

        ll power = 1, count = 0;

        for (ll j = 0; j < n; ++j) {

            count += abs(a[j] - power);
            if (j != n - 1)
                power = power * (ll)i;

            // If exceeds maximum value
            if (power >= 1e10)
                break;
        }

        if (power >= (1e10)
            || power > (ll)(sum - n)
                           + a[n - 1])
            break;

        // Update minimum moves
        if (minmove > count) {
            minmove = count;
            K = i;
        }
    }

    // Print K corresponds to minimum
    // number of moves
    cout << K;
}

// Driver Code
int main()
{

    // Given vector
    vector<ll> a = { 1, 9, 27 };

    // Function Call
    findMinCostInteger(a);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the value of K such
// that it takes minimum number of moves
// to convert the array in its power
static void findMinCostInteger(int a[], int n)
{

    // Finding tha sum of the array
    int sum = 0;
    for(int i = 0; i < n; i++)
        sum += a[i];

    int K = 0, minmove = Integer.MAX_VALUE;

    // Find K for which the count
    // of moves will become minimum
    for(int i = 1;; ++i)
    {
        int power = 1, count = 0;

        for(int j = 0; j < n; ++j)
        {
            count += Math.abs(a[j] - power);

            if (j != n - 1)
                power = power * i;

            // If exceeds maximum value
            if (power >= 1e10)
                break;
        }

        if (power >= (1e10) ||
            power > (sum - n) + a[n - 1])
            break;

        // Update minimum moves
        if (minmove > count)
        {
            minmove = count;
            K = i;
        }
    }

    // Print K corresponds to minimum
    // number of moves
    System.out.println(K);
}

// Driver Code
public static void main(String args[])
{

    // Given vector
    int []a = { 1, 9, 27 };

    // Function Call
    findMinCostInteger(a, 3);
}
}

// This code is contributed by bgangwar59
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to find the value of K such
# that it takes minimum number of moves
# to convert the array in its power
def findMinCostInteger(a):

    # Size of the array
    n = len(a)

    # Finding tha sm of the array
    sm = sum(a)

    K = 0
    minmove = sys.maxsize

    # Find K for which the count
    # of moves will become minimum
    i = 1
    while(1):
        power = 1
        count = 0
        for j in range(n):
            count += abs(a[j] - power)

            if (j != n - 1):
                power = power * i

            # If exceeds maximum value
            if (power >= 1e10):
                break

        if (power >= (1e10) or
            power > (sm - n) + a[n - 1]):
            break

        # Update minimum moves
        if (minmove > count):
            minmove = count
            K = i

        i += 1

    # Print K corresponds to minimum
    # number of moves
    print(K)

# Driver Code
if __name__ == '__main__':

    # Given vector
    a =  [ 1, 9, 27 ]

    # Function Call
    findMinCostInteger(a)

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the
// above approach
using System;
class GFG{

// Function to find the value
// of K such that it takes
// minimum number of moves
// to convert the array in
// its power
static void findMinCostint(int []a,
                           int n)
{   
  // Finding tha sum of the array
  int sum = 0;

  for(int i = 0; i < n; i++)
    sum += a[i];

  int K = 0, minmove = int.MaxValue;

  // Find K for which the count
  // of moves will become minimum
  for(int i = 1;; ++i)
  {
    int power = 1, count = 0;

    for(int j = 0; j < n; ++j)
    {
      count += Math.Abs(a[j] - power);

      if (j != n - 1)
        power = power * i;

      // If exceeds maximum value
      if (power >= 1e10)
        break;
    }

    if (power >= (1e10) ||
        power > (sum - n) +
                 a[n - 1])
      break;

    // Update minimum moves
    if (minmove > count)
    {
      minmove = count;
      K = i;
    }
  }

  // Print K corresponds to
  // minimum number of moves
  Console.WriteLine(K);
}

// Driver Code
public static void Main(String []args)
{   
  // Given vector
  int []a = {1, 9, 27};

  // Function Call
  findMinCostint(a, 3);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the value of K such
// that it takes minimum number of moves
// to convert the array in its power
function findMinCostLeteger(a, n)
{

    // Finding tha sum of the array
    let sum = 0;
    for(let i = 0; i < n; i++)
        sum += a[i];

    let K = 0, minmove = Number.MAX_VALUE;

    // Find K for which the count
    // of moves will become minimum
    for(let i = 1;; ++i)
    {
        let power = 1, count = 0;

        for(let j = 0; j < n; ++j)
        {
            count += Math.abs(a[j] - power);

            if (j != n - 1)
                power = power * i;

            // If exceeds maximum value
            if (power >= 1e10)
                break;
        }

        if (power >= (1e10) ||
            power > (sum - n) + a[n - 1])
            break;

        // Update minimum moves
        if (minmove > count)
        {
            minmove = count;
            K = i;
        }
    }

    // Print K corresponds to minimum
    // number of moves
    document.write(K);
}

// Driver Code

// Given vector
let a = [ 1, 9, 27 ];

// Function Call
findMinCostLeteger(a, 3);

// This code is contributed by souravghosh0416

</script>
```

**Output**

```
5
```

***时间复杂度:** O(N * max(x))*
***辅助空间:** O(1)*