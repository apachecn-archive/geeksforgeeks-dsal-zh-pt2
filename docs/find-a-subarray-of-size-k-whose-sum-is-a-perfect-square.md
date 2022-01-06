# 找到一个大小为 K 的子阵列，其和为一个完美的正方形

> 原文:[https://www . geeksforgeeks . org/find-a-subarray-of-size-k-其和是一个完美的正方形/](https://www.geeksforgeeks.org/find-a-subarray-of-size-k-whose-sum-is-a-perfect-square/)

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和一个整数 **K** ，任务是找到一个长度为 **K** 的子数组，其和为[完美平方](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)。如果不存在这样的子阵列，则打印 **-1** 。否则，打印子阵列。

**注意:**可以有多个可能的子阵列。打印其中任何一个。
**例:**

> **输入:** arr[] = {20，34，51，10，99，87，23，45}，K = 3
> **输出:** {10，99，87}
> **说明:**子阵{10，99，87}元素之和为 196，是一个完美的正方形(16 <sup>2</sup> = 196)。
> 
> **输入:** arr[] = {20，34，51，10，99，87，23，45}，K = 4
> **输出:** -1
> **说明:**大小为 K 的子阵没有一个和是完美平方的。

**天真法:**解决问题最简单的方法是[生成所有可能的子阵](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)大小 **K** 检查生成的任何子阵之和是否为[完美平方](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)。如果发现是真的，打印那个子阵列。如果没有满足条件的子阵列，打印**-1”**。
***时间复杂度:** O(N*K)*
***辅助空间:** O(K)*

**有效方法:**一种有效方法是使用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)来寻找大小为 **K** 的连续子阵列的和，然后使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)来检查该和是否是完美平方。下面是解决这个问题的步骤:

1.  计算第一个 **K** 数组元素的和，并将其存储在一个变量中，比如 **curr_sum** 。
2.  然后逐个迭代剩余的数组元素，通过增加 **i <sup>第</sup>元素**并从数组中移除**(I–K)<sup>第</sup>元素**来更新 **curr_sum** 。
3.  对于获得的每一个 **curr_sum** 值，检查它是否是一个[完美平方](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)数。
4.  如果发现 **curr_sum** 的任何值为真，则打印相应的子阵列。
5.  否则，打印-1。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if a given number
// is a perfect square or not
bool isPerfectSquare(int n)
{
    // Find square root of n
    double sr = sqrt(n);

    // Check if the square root
    // is an integer or not
    return ((sr - floor(sr)) == 0);
}

// Function to print the subarray
// whose sum is a perfect square
void SubarrayHavingPerfectSquare(
    vector<int> arr, int k)
{
    pair<int, int> ans;
    int sum = 0, i;

    // Sum of first K elements
    for (i = 0; i < k; i++) {
        sum += arr[i];
    }

    bool found = false;

    // If the first k elements have
    // a sum as perfect square
    if (isPerfectSquare(sum)) {
        ans.first = 0;
        ans.second = i - 1;
    }
    else {

        // Iterate through the array
        for (int j = i;
             j < arr.size(); j++) {

            sum = sum + arr[j] - arr[j - k];

            // If sum is perfect square
            if (isPerfectSquare(sum)) {
                found = true;
                ans.first = j - k + 1;
                ans.second = j;
            }
        }

        for (int k = ans.first;
             k <= ans.second; k++) {
            cout << arr[k] << " ";
        }
    }

    // If subarray not found
    if (found == false) {
        cout << "-1";
    }
}

// Driver Code
int main()
{
    // Given array
    vector<int> arr;

    arr = { 20, 34, 51, 10,
            99, 87, 23, 45 };

    // Given subarray size K
    int K = 3;

    // Function Call
    SubarrayHavingPerfectSquare(arr, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
class GFG{

static class pair
{
  int first, second;
}
// Function to check if a given number
// is a perfect square or not
static boolean isPerfectSquare(int n)
{
  // Find square root of n
  double sr = Math.sqrt(n);

  // Check if the square root
  // is an integer or not
  return ((sr - Math.floor(sr)) == 0);
}

// Function to print the subarray
// whose sum is a perfect square
static void SubarrayHavingPerfectSquare(int[] arr,
                                        int k)
{
  pair ans = new pair();
  int sum = 0, i;

  // Sum of first K elements
  for (i = 0; i < k; i++)
  {
    sum += arr[i];
  }

  boolean found = false;

  // If the first k elements have
  // a sum as perfect square
  if (isPerfectSquare(sum))
  {
    ans.first = 0;
    ans.second = i - 1;
  }
  else
  {
    // Iterate through the array
    for (int j = i; j < arr.length; j++)
    {
      sum = sum + arr[j] - arr[j - k];

      // If sum is perfect square
      if (isPerfectSquare(sum))
      {
        found = true;
        ans.first = j - k + 1;
        ans.second = j;
      }
    }

    for (int k1 = ans.first;
             k1 <= ans.second; k1++)
    {
      System.out.print(arr[k1] + " ");
    }
  }

  // If subarray not found
  if (found == false)
  {
    System.out.print("-1");
  }
}

// Driver Code
public static void main(String[] args)
{
  // Given array
  int []arr = {20, 34, 51, 10,
               99, 87, 23, 45};

  // Given subarray size K
  int K = 3;

  // Function Call
  SubarrayHavingPerfectSquare(arr, K);

}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import sqrt, ceil, floor

# Function to check if a given number
# is a perfect square or not
def isPerfectSquare(n):

    # Find square root of n
    sr = sqrt(n)

    # Check if the square root
    # is an integer or not
    return ((sr - floor(sr)) == 0)

# Function to print the subarray
# whose sum is a perfect square
def SubarrayHavingPerfectSquare(arr, k):

    ans = [ 0, 0 ]
    sum = 0

    # Sum of first K elements
    i = 0
    while i < k:
        sum += arr[i]
        i += 1

    found = False

    # If the first k elements have
    # a sum as perfect square
    if (isPerfectSquare(sum)):
        ans[0] = 0
        ans[1] = i - 1

    else:

        # Iterate through the array
        for j in range(i, len(arr)):
            sum = sum + arr[j] - arr[j - k]

            # If sum is perfect square
            if (isPerfectSquare(sum)):
                found = True
                ans[0] = j - k + 1
                ans[1] = j

        for k in range(ans[0], ans[1] + 1):
            print(arr[k], end = " ")

    # If subarray not found
    if (found == False):
        print("-1")

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [ 20, 34, 51, 10,
            99, 87, 23, 45 ]

    # Given subarray size K
    K = 3

    # Function call
    SubarrayHavingPerfectSquare(arr, K)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

class pair
{
  public int first, second;
}

// Function to check if a given number
// is a perfect square or not
static bool isPerfectSquare(int n)
{
  // Find square root of n
  double sr = Math.Sqrt(n);

  // Check if the square root
  // is an integer or not
  return ((sr - Math.Floor(sr)) == 0);
}

// Function to print the subarray
// whose sum is a perfect square
static void SubarrayHavingPerfectSquare(int[] arr,
                                        int k)
{
  pair ans = new pair();
  int sum = 0, i;

  // Sum of first K elements
  for (i = 0; i < k; i++)
  {
    sum += arr[i];
  }

  bool found = false;

  // If the first k elements have
  // a sum as perfect square
  if (isPerfectSquare(sum))
  {
    ans.first = 0;
    ans.second = i - 1;
  }
  else
  {
    // Iterate through the array
    for (int j = i; j < arr.Length; j++)
    {
      sum = sum + arr[j] - arr[j - k];

      // If sum is perfect square
      if (isPerfectSquare(sum))
      {
        found = true;
        ans.first = j - k + 1;
        ans.second = j;
      }
    }

    for (int k1 = ans.first;
             k1 <= ans.second; k1++)
    {
      Console.Write(arr[k1] + " ");
    }
  }

  // If subarray not found
  if (found == false)
  {
    Console.Write("-1");
  }
}

// Driver Code
public static void Main(String[] args)
{
  // Given array
  int []arr = {20, 34, 51, 10,
               99, 87, 23, 45};

  // Given subarray size K
  int K = 3;

  // Function Call
  SubarrayHavingPerfectSquare(arr, K);

}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check if a given number
// is a perfect square or not
function isPerfectSquare(n)
{
    // Find square root of n
    var sr = Math.sqrt(n);

    // Check if the square root
    // is an integer or not
    return ((sr - Math.floor(sr)) == 0);
}

// Function to print the subarray
// whose sum is a perfect square
function SubarrayHavingPerfectSquare( arr, k)
{
    var ans = [];
    var sum = 0, i;

    // Sum of first K elements
    for (i = 0; i < k; i++) {
        sum += arr[i];
    }

    var found = false;

    // If the first k elements have
    // a sum as perfect square
    if (isPerfectSquare(sum)) {
        ans[0] = 0;
        ans[1] = i - 1;
    }
    else {

        // Iterate through the array
        for (var j = i;
             j < arr.length; j++) {

            sum = sum + arr[j] - arr[j - k];

            // If sum is perfect square
            if (isPerfectSquare(sum)) {
                found = true;
                ans[0] = j - k + 1;
                ans[1] = j;
            }
        }

        for (var k = ans[0];
             k <= ans[1]; k++) {
            document.write( arr[k] + " ");
        }
    }

    // If subarray not found
    if (found == false) {
        document.write( "-1");
    }
}

// Driver Code
// Given array
var arr = [20, 34, 51, 10,
        99, 87, 23, 45 ];
// Given subarray size K
var K = 3;
// Function Call
SubarrayHavingPerfectSquare(arr, K);

</script>
```

**Output:** 

```
10 99 87
```

***时间复杂度:**O(N * log(sum))*
***辅助空间:** O(1)*