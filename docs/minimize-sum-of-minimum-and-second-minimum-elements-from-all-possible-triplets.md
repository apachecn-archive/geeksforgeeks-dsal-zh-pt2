# 最小化所有可能三元组的最小和第二最小元素的总和

> 原文:[https://www . geeksforgeeks . org/从所有可能的三元组中最小化最小和第二最小元素之和/](https://www.geeksforgeeks.org/minimize-sum-of-minimum-and-second-minimum-elements-from-all-possible-triplets/)

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是最小化所有可能三元组的最小和第二最小元素的总和。一个元素可以恰好是一个三元组的一部分。

> **输入:** arr[] = {1，2，4，6，7，8，3}，N = 7
> **输出:** 10
> **说明:**这里形成两个三元组，因为 arr[]的大小是 7，7/3 = 2。
> 三元组 1 –{ 1，6，3} - >两个最小元素是 1 和 3。
> 三元组 2 –{ 2，4，8} - >两个最小元素是 2 和 4。
> 因此总和= 1 + 3 + 2 + 4 = 10
> 
> **输入:** arr[] = {5，7，3，8，9}
> **输出:** 8

**进场:**这个问题可以用[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)解决。按照以下步骤解决给定的问题。

*   按照**不递减的**顺序对数组 **arr[]** 进行排序，这样可以更容易地选择每个三元组中的最小元素。
*   初始化一个变量，比如 **ans = 0** ，以存储最小可能的答案。
*   遍历 **arr[]** ，取左侧两个元素，右侧一个元素，组成每个三元组。
*   返回 **ans** 作为最终答案。

## C++14

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to minimize answer after choosing
// all the triplets from arr[]
int minTriplets(vector<int>& arr, int N)
{

    // To store the final answer
    int ans = 0;

    // Sort the array
    sort(arr.begin(), arr.end());

    // Traverse the array
    for (int i = 0, j = N - 1;
         i + 1 < j;
         i += 2, j--) {

        // Add both the smallest numbers
        // of current triplet
        ans += arr[i];
        ans += arr[i + 1];
    }

    // Return the ans as the required answer
    return ans;
}

// Driver Code
int main()
{
    int N = 7;

    vector<int> arr = { 1, 2, 4, 6, 7, 8, 3 };

    cout << minTriplets(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.util.*;
public class GFG
{

  // Function to minimize answer after choosing
  // all the triplets from arr[]
  static int minTriplets(int []arr, int N)
{

  // To store the final answer
  int ans = 0;

  // Sort the array
  Arrays.sort(arr);

  // Traverse the array
  for (int i = 0, j = N - 1;
       i + 1 < j;
       i += 2, j--) {

    // Add both the smallest numbers
    // of current triplet
    ans += arr[i];
    ans += arr[i + 1];
  }

  // Return the ans as the required answer
  return ans;
}

// Driver Code
public static void main(String args[])
{
  int N = 7;

  int []arr = { 1, 2, 4, 6, 7, 8, 3 };

  System.out.print(minTriplets(arr, N));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# Python program for above approach

# Function to minimize answer after choosing
# all the triplets from arr[]
def minTriplets (arr, N) :

    # To store the final answer
    ans = 0

    # Sort the array
    arr.sort()

    i = 0
    j = N - 1

    # Traverse the array
    while( i + 1 < j):

        # Add both the smallest numbers
        # of current triplet
        ans += arr[i]
        ans += arr[i + 1]
        i += 2
        j -= 1

    # Return the ans as the required answer
    return ans

# Driver Code
N = 7
arr = [1, 2, 4, 6, 7, 8, 3]
print(minTriplets(arr, N))

# This code is contributed by gfgking
```

## C#

```
// C# program for above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG
{

// Function to minimize answer after choosing
// all the triplets from arr[]
static int minTriplets(int []arr, int N)
{

    // To store the final answer
    int ans = 0;

    // Sort the array
    Array.Sort(arr);

    // Traverse the array
    for (int i = 0, j = N - 1;
         i + 1 < j;
         i += 2, j--) {

        // Add both the smallest numbers
        // of current triplet
        ans += arr[i];
        ans += arr[i + 1];
    }

    // Return the ans as the required answer
    return ans;
}

// Driver Code
public static void Main()
{
    int N = 7;
    int []arr = { 1, 2, 4, 6, 7, 8, 3 };
    Console.Write(minTriplets(arr, N));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
    // JavaScript program for above approach

    // Function to minimize answer after choosing
    // all the triplets from arr[]
    const minTriplets = (arr, N) => {

        // To store the final answer
        let ans = 0;

        // Sort the array
        arr.sort();

        // Traverse the array
        for (let i = 0, j = N - 1;
            i + 1 < j;
            i += 2, j--) {

            // Add both the smallest numbers
            // of current triplet
            ans += arr[i];
            ans += arr[i + 1];
        }

        // Return the ans as the required answer
        return ans;
    }

    // Driver Code

    let N = 7;

    let arr = [1, 2, 4, 6, 7, 8, 3];

    document.write(minTriplets(arr, N));

    // This code is contributed by rakeshsahni

</script>
```

**Output**

```
10
```

**时间复杂度:**O(N log N)
T3】辅助空间: O(1)