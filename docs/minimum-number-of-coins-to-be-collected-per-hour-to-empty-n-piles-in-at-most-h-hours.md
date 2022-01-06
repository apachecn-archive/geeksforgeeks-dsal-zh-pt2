# 最多 H 小时内每小时收集的清空 N 堆硬币的最小数量

> 原文:[https://www . geeksforgeeks . org/每小时最少要收集的硬币数量-最多 h 小时空 n 堆/](https://www.geeksforgeeks.org/minimum-number-of-coins-to-be-collected-per-hour-to-empty-n-piles-in-at-most-h-hours/)

给定一个由代表每堆硬币数量的 **N** 个整数和一个整数 **H** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】【】**，任务是找到每小时必须从单堆收集的硬币的最小数量，使得所有堆在不到 **H** 个小时内被清空。

***注:**一小时内只能从单堆中收集硬币。*

**示例:**

> **输入:** arr[] = {3，6，7，11}，H = 8
> **输出:** 4
> **说明:**
> 每小时每堆取出 4 枚硬币，清空每堆所用时间如下:
> arr[0]= 3:1 小时清空。
> arr[1] =第 1 小时取出 6: 4 枚硬币，第 2 小时取出 2 枚硬币。因此，在 2 小时内清空。
> arr[2] = 7:第 1 小时取出 4 枚硬币，第 2 小时取出 3 枚硬币。因此，在 2 小时内清空。
> arr[3] = 11:第 1 小时和第 2 小时移除 4 枚硬币，第 3 小时移除 3 枚硬币。因此，在 3 小时内清空。
> 因此，所需小时数= 1 + 2 + 2 + 3 = 8 ( = H)。
> 
> **输入:** arr[] = {30，11，23，4，20}，H = 5
> **输出:** 30

**进场:**思路是用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)。按照以下步骤解决问题:

*   初始化一个变量，比如**和**，来存储每小时需要收集的最小硬币数。
*   将变量**低电平**和**高电平**初始化为 1 和数组中的[最大值，以设置执行](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)[二分搜索法](https://www.geeksforgeeks.org/binary-search/)的范围。
*   重复直到**低≤高**并执行以下步骤:
    *   求**中间**的值为**(低+高)/2** 。
    *   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**找到每小时取出**中**硬币清空所有硬币堆所需的时间，并检查总时间是否超过 **H** 。如果发现为假，将高更新为**(K–1)**，将 **ans** 更新为 **K** 。否则，将**低电平**更新为 **(K + 1)** 。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of coins to be collected per hour
// to empty N piles in H hours
int minCollectingSpeed(vector<int>& piles,
                       int H)
{
    // Stores the minimum coins
    // to be removed per hour
    int ans = -1;

    int low = 1, high;

    // Find the maximum array element
    high = *max_element(piles.begin(),
                        piles.end());

    // Perform Binary Search
    while (low <= high)

    {
        // Store the mid value of the
        // range in K
        int K = low + (high - low) / 2;

        int time = 0;

        // Find the total time taken to
        // empty N piles by removing K
        // coins per hour
        for (int ai : piles) {

            time += (ai + K - 1) / K;
        }

        // If total time does not exceed H
        if (time <= H) {
            ans = K;
            high = K - 1;
        }

        // Otherwise
        else {
            low = K + 1;
        }
    }

    // Print the required result
    cout << ans;
}

// Driver Code
int main()
{
    vector<int> arr = { 3, 6, 7, 11 };
    int H = 8;

    // Function Call
    minCollectingSpeed(arr, H);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the minimum number
// of coins to be collected per hour
// to empty N piles in H hours
static void minCollectingSpeed(int[] piles,
                               int H)
{

    // Stores the minimum coins
    // to be removed per hour
    int ans = -1;

    int low = 1, high;

    // Find the maximum array element
    high = Arrays.stream(piles).max().getAsInt();

    // Perform Binary Search
    while (low <= high)
    {

        // Store the mid value of the
        // range in K
        int K = low + (high - low) / 2;

        int time = 0;

        // Find the total time taken to
        // empty N piles by removing K
        // coins per hour
        for(int ai : piles)
        {
            time += (ai + K - 1) / K;
        }

        // If total time does not exceed H
        if (time <= H)
        {
            ans = K;
            high = K - 1;
        }

        // Otherwise
        else
        {
            low = K + 1;
        }
    }

    // Print the required result
    System.out.print(ans);
}

// Driver Code
static public void main(String args[])
{
    int[] arr = { 3, 6, 7, 11 };
    int H = 8;

    // Function Call
    minCollectingSpeed(arr, H);
}
}

// This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;

class GFG
{

  // Function to find the minimum number
  // of coins to be collected per hour
  // to empty N piles in H hours
  static void minCollectingSpeed(int[] piles,
                                 int H)
  {

    // Stores the minimum coins
    // to be removed per hour
    int ans = -1;   
    int low = 1, high;    
    Array.Sort(piles);

    // Find the maximum array element
    high = piles[piles.Length - 1 ];

    // Perform Binary Search
    while (low <= high)
    {

      // Store the mid value of the
      // range in K
      int K = low + (high - low) / 2;

      int time = 0;

      // Find the total time taken to
      // empty N piles by removing K
      // coins per hour
      foreach(int ai in piles)
      {
        time += (ai + K - 1) / K;
      }

      // If total time does not exceed H
      if (time <= H)
      {
        ans = K;
        high = K - 1;
      }

      // Otherwise
      else
      {
        low = K + 1;
      }
    }

    // Print the required result
    Console.Write(ans);
  }

  // Driver Code
  static public void Main(string []args)
  {
    int[] arr = { 3, 6, 7, 11 };
    int H = 8;

    // Function Call
    minCollectingSpeed(arr, H);
  }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum number
# of coins to be collected per hour
# to empty N piles in H hours
def minCollectingSpeed(piles, H):

    # Stores the minimum coins
    # to be removed per hour
    ans = -1
    low = 1

    # Find the maximum array element
    high = max(piles)

    # Perform Binary Search
    while (low <= high):

        # Store the mid value of the
        # range in K
        K = low + (high - low) // 2

        time = 0

        # Find the total time taken to
        # empty N piles by removing K
        # coins per hour
        for ai in piles:
          time += (ai + K - 1) // K

        # If total time does not exceed H
        if (time <= H):
            ans = K
            high = K - 1

        # Otherwise
        else:
            low = K + 1

    # Print required result
    print(ans)

# Driver Code
if __name__ == '__main__':
    arr = [3, 6, 7, 11]
    H = 8

    # Function Call
    minCollectingSpeed(arr, H)

# This code is contributed by  mohit kumar 29
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the minimum number
// of coins to be collected per hour
// to empty N piles in H hours
function minCollectingSpeed(piles, H)
{
    // Stores the minimum coins
    // to be removed per hour
    var ans = -1;

    var low = 1, high;

    // Find the maximum array element
    high = piles.reduce((a,b)=> Math.max(a,b));

    // Perform Binary Search
    while (low <= high)

    {
        // Store the mid value of the
        // range in K
        var K = low + parseInt((high - low) / 2);

        var time = 0;

        // Find the total time taken to
        // empty N piles by removing K
        // coins per hour
        piles.forEach(ai => {

            time += parseInt((ai + K - 1) / K);
        });

        // If total time does not exceed H
        if (time <= H) {
            ans = K;
            high = K - 1;
        }

        // Otherwise
        else {
            low = K + 1;
        }
    }

    // Print the required result
    document.write( ans);
}

// Driver Code
var arr = [3, 6, 7, 11];
var H = 8;
// Function Call
minCollectingSpeed(arr, H);

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(H*log N)*
***辅助空间:** O(1)*