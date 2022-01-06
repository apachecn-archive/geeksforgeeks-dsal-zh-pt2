# 从原点

开始后，访问 X 轴上给定 K 点的最小距离

> 原文:[https://www . geesforgeks . org/从原点出发后 x 轴上给定 k 点的最小访问距离/](https://www.geeksforgeeks.org/minimum-distance-to-visit-given-k-points-on-x-axis-after-starting-from-the-origin/)

给定一个大小为 **N** 的[排序数组](https://www.geeksforgeeks.org/program-check-array-sorted-not-iterative-recursive/)、 **arr[]** ，代表 **X-** 轴上第 **i <sup>第</sup>T9】点的位置和一个整数 **K** ，任务是找到从 **X** 轴原点开始访问 **K** 点所需的最小距离。**

**示例:**

> **输入:** arr[]={-30，-10，10，20，50}，K = 3
> **输出:** 40
> **说明:**
> 从原点移动到第二点。因此，总行驶距离= 10。
> 从第二点移动到第三点。因此，总行程= 10 + 10 = 20
> 从第三点移动到第四点。因此，总行程= 20 + 20 = 40
> 因此，访问 K 点的总行程为 40。
> 
> **输入:** arr[]={-1，-5，-4，-3，6}，K = 3
> T3】输出: 6

**方法:**访问每个 **K** 连续点，打印访问 **K** 连续点的最小行程距离，即可解决问题。按照以下步骤解决问题:

*   初始化一个变量，比如 **res** ，来存储访问 **K** 点的最小行程距离。
*   初始化一个变量，比如 **dist** ，来存储访问 **K** 点所经过的距离。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并检查以下条件。
    *   如果 **(arr[i] > = 0 且 arr[i + K -1] > = 0)** 的值为真，则更新 **dist = max(arr[i]，arr[i + K -1])。**
    *   否则，**距离= ABS(arr[I])+ABS(arr[I+k-1])+min(arr[I])、ABS(arr[I+k-1)]**。
    *   最后，更新 **res = min(res，dist)** 。
*   最后，打印 **res** 的值。

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum distance 
// travelled to visit K point
int MinDistK(int arr[], int N, int K)
{

    // Stores minimum distance travelled
    // to visit K point
    int res = INT_MAX;

    // Stores distance travelled
    // to visit points
    int dist = 0;

    // Traverse the array arr[]
    for (int i = 0; i <= (N - K); i++) {

       // If arr[i] and arr[i + K - 1]
       // are positive
        if (arr[i] >= 0  && 
              arr[i + K - 1] >= 0) {

            // Update dist
            dist = max(arr[i], arr[i + K - 1]);
        }
        else {

            // Update dist
            dist = abs(arr[i]) +
                   abs(arr[i + K - 1])
                  + min(abs(arr[i]),
                        abs(arr[i + K - 1]));
        }

        // Update res
        res = min(res, dist);
    }

    return res;
}

// Driver Code
int main()
{

    int K = 3;
    // initial the array
    int arr[] = { -30, -10, 10, 20, 50 };

    int N = sizeof(arr) / sizeof(arr[0]);

    cout<< MinDistK(arr, N, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class solution{

// Function to find the minimum
// distance travelled to visit
// K point
static int MinDistK(int arr[],
                    int N, int K)
{      
  // Stores minimum distance
  // travelled to visit K point
  int res = Integer.MAX_VALUE;

  // Stores distance travelled
  // to visit points
  int dist = 0;

  // Traverse the array arr[]
  for (int i = 0;
           i <= (N - K); i++)
  {
    // If arr[i] and arr[i + K - 1]
    // are positive
    if (arr[i] >= 0  && 
        arr[i + K - 1] >= 0)
    {
      // Update dist
      dist = Math.max(arr[i],
                      arr[i + K - 1]);
    }
    else
    {
      // Update dist
      dist = Math.abs(arr[i]) +
             Math.abs(arr[i + K - 1]) +
             Math.min(Math.abs(arr[i]),
             Math.abs(arr[i + K - 1]));
    }

    // Update res
    res = Math.min(res, dist);
  }

  return res;
}

// Driver Code
public static void main(String args[])
{
  int K = 3;
  // initial the array
  int arr[] = {-30, -10,
               10, 20, 50};

  int N = arr.length;
  System.out.println(MinDistK(arr, N, K));
}
}

// This code is contributed by bgangwar59
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
import sys

# Function to find the minimum distance 
# travelled to visit K point
def MinDistK(arr, N, K):

    # Stores minimum distance travelled
    # to visit K point
    res = sys.maxsize

    # Stores distance travelled
    # to visit points
    dist = 0

    # Traverse the array arr[]
    for i in range(N - K + 1):

        # If arr[i] and arr[i + K - 1]
        # are positive
        if (arr[i] >= 0 and arr[i + K - 1] >= 0):

            # Update dist
            dist = max(arr[i], arr[i + K - 1])
        else:

            # Update dist
            dist = (abs(arr[i]) + abs(arr[i + K - 1]) +
                min(abs(arr[i]), abs(arr[i + K - 1])))

        # Update res
        res = min(res, dist)

    return res

# Driver Code
if __name__ == '__main__':

    K = 3

    # Initial the array
    arr = [ -30, -10, 10, 20, 50 ]

    N = len(arr)

    print(MinDistK(arr, N, K))

# This code is contributed by ipg2016107
```

## C#

```
// C# program to implement
// the above approach 
using System;

class GFG{

// Function to find the minimum
// distance travelled to visit
// K point
static int MinDistK(int[] arr,
                    int N, int K)
{ 

  // Stores minimum distance
  // travelled to visit K point
  int res = Int32.MaxValue;

  // Stores distance travelled
  // to visit points
  int dist = 0;

  // Traverse the array arr[]
  for(int i = 0; i <= (N - K); i++)
  {

    // If arr[i] and arr[i + K - 1]
    // are positive
    if (arr[i] >= 0 && 
        arr[i + K - 1] >= 0)
    {

      // Update dist
      dist = Math.Max(arr[i],
                      arr[i + K - 1]);
    }
    else
    {

      // Update dist
      dist = Math.Abs(arr[i]) +
             Math.Abs(arr[i + K - 1]) +
             Math.Min(Math.Abs(arr[i]),
             Math.Abs(arr[i + K - 1]));
    }

    // Update res
    res = Math.Min(res, dist);
  }
  return res;
}

// Driver Code
public static void Main()
{
  int K = 3;

  // Initial the array
  int[] arr = { -30, -10, 10, 20, 50};

  int N = arr.Length;

  Console.WriteLine(MinDistK(arr, N, K));
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to find the minimum
// distance travelled to visit
// K point
function MinDistK(arr, N, K)
{     
  // Stores minimum distance
  // travelled to visit K point
  let res = Number.MAX_VALUE;

  // Stores distance travelled
  // to visit points
  let dist = 0;

  // Traverse the array arr[]
  for (let i = 0;
           i <= (N - K); i++)
  {
    // If arr[i] and arr[i + K - 1]
    // are positive
    if (arr[i] >= 0  &&
        arr[i + K - 1] >= 0)
    {
      // Update dist
      dist = Math.max(arr[i],
                      arr[i + K - 1]);
    }
    else
    {
      // Update dist
      dist = Math.abs(arr[i]) +
             Math.abs(arr[i + K - 1]) +
             Math.min(Math.abs(arr[i]),
             Math.abs(arr[i + K - 1]));
    }

    // Update res
    res = Math.min(res, dist);
  }

  return res;
}

// Driver Code

    let K = 3;
  // initial the array
  let arr = [-30, -10,
               10, 20, 50];

  let N = arr.length;
  document.write(MinDistK(arr, N, K));

</script>
```

**Output**

```
40
```