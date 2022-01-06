# 通过将 arr[i]移动到 index arr[i]

来再次访问同一索引所需的通过次数

> 原文:[https://www . geeksforgeeks . org/通过移动到索引的方式再次访问相同索引所需的通过次数/](https://www.geeksforgeeks.org/count-of-pass-required-to-visit-same-index-again-by-moving-arri-to-index-arri/)

给定第一个 **N** [自然数](https://www.geeksforgeeks.org/natural-numbers/)排列的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)(基于 1 的索引)**arr【】**，每个元素的任务是找到达到该索引所需的移动次数，使得在每次移动中，索引 **i** 处的数组元素移动到索引**arr【I】**处的数组元素。

**示例:**

> **输入:** arr[] = {2，3，1}
> **输出:** 3 3 3
> **解释:**
> 对于数组元素 arr[1] = 2，索引的移动集为 1 - > 2 - > 3 - > 1。所需的移动总数为 3。
> 对于数组元素 arr[2] = 3，索引的移动集为 2 - > 3 - > 1 - > 2。所需的移动总数为 3。
> 对于数组元素 arr[3] = 1，索引的移动集为 3 - > 1 - > 2 - > 3。所需的移动总数为 3。
> 
> **输入:** arr[] = {4，6，2，1，5，3 }
> T3】输出:2 3 2 1 3

**方法:**给定的问题可以通过找到每个索引的每个数组元素所需的移动次数来解决。按照以下步骤解决给定的问题:

*   [使用变量 **i** 遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，并执行以下步骤:
    *   初始化一个变量，比如说**计数**，它存储了需要移动的总次数。
    *   初始化一个变量，称 **K** 为 **i** ，迭代一个[边做边循环](https://www.geeksforgeeks.org/c-c-do-while-loop-with-examples/)，在该循环中更新 **K** 的值为**arr【K】**，将 **count** 的值增加 **1** ，直到 **K** 与 **i** 的值不相同。
    *   完成上述步骤后，打印**计数**的值，作为当前索引所需的移动的结果计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the number of moves
// required to visit the same index
// again for every array element
void numberOfPasses(vector<int> arr, int N)
{
    // Make given array 0 index based
    for (int i = 0; i < N; ++i) {
        --arr[i];
    }

    for (int i = 0; i < N; ++i) {

        // Stores the number of moves
        int cnt = 0;

        // Store index value
        int k = i;

        do {

            // Update the value of cnt
            ++cnt;

            // Make a pass
            k = arr[k];

        } while (k != i);

        // Print the value of cnt
        cout << cnt << " ";
    }
}

// Driver Code
int main()
{
    vector<int> arr{ 4, 6, 2, 1, 5, 3 };
    int N = arr.size();
    numberOfPasses(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG
{

  // Function to find the number of moves
  // required to visit the same index
  // again for every array element
  static void numberOfPasses(int[] arr, int N)
  {

    // Make given array 0 index based
    for (int i = 0; i < N; ++i) {
      --arr[i];
    }

    for (int i = 0; i < N; ++i) {

      // Stores the number of moves
      int cnt = 0;

      // Store index value
      int k = i;

      do {

        // Update the value of cnt
        ++cnt;

        // Make a pass
        k = arr[k];

      } while (k != i);

      // Print the value of cnt
      System.out.print(cnt+" ");
    }
  }

  // Driver Code
  public static void main (String[] args)
  {
    int[] arr = { 4, 6, 2, 1, 5, 3 };
    int N = arr.length;
    numberOfPasses(arr, N);

  }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the number of moves
# required to visit the same index
# again for every array element
def numberOfPasses(arr, N):

    # Make given array 0 index based
    for i in range(0, N): 
        arr[i] = arr[i] - 1

    for i in range(0, N):

        # Stores the number of moves
        cnt = 0;

        # Store index value
        k = i;

        while(True):

            # Update the value of cnt
            cnt = cnt + 1

            # Make a pass
            k = arr[k]

            if (k == i):
                break;

        # Print the value of cnt
        print(cnt, end=" ")

# Driver Code

arr = [4, 6, 2, 1, 5, 3]
N = len(arr)
numberOfPasses(arr, N)

# This code is contributed by ihritik
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the number of moves
// required to visit the same index
// again for every array element
static void numberOfPasses(int []arr, int N)
{

    // Make given array 0 index based
    for (int i = 0; i < N; ++i) {
        --arr[i];
    }

    for (int i = 0; i < N; ++i) {

    // Stores the number of moves
    int cnt = 0;

    // Store index value
    int k = i;

    do {
        // Update the value of cnt
        ++cnt;

        // Make a pass
        k = arr[k];

    } while (k != i);

    // Print the value of cnt
    Console.Write(cnt + " ");
    }
}

// Driver Code
public static void Main()
{
    int []arr = { 4, 6, 2, 1, 5, 3 };
    int N = arr.Length;
    numberOfPasses(arr, N);
}
}

// This code is contributed by Samim Hossain Mondal
```

## java 描述语言

```
<script>
    // JavaScript program for the above approach

    // Function to find the number of moves
    // required to visit the same index
    // again for every array element
    const numberOfPasses = (arr, N) => {
        // Make given array 0 index based
        for (let i = 0; i < N; ++i) {
            --arr[i];
        }

        for (let i = 0; i < N; ++i) {

            // Stores the number of moves
            let cnt = 0;

            // Store index value
            let k = i;

            do {

                // Update the value of cnt
                ++cnt;

                // Make a pass
                k = arr[k];

            } while (k != i);

            // Print the value of cnt
            document.write(`${cnt} `);
        }
    }

    // Driver Code
    let arr = [4, 6, 2, 1, 5, 3];
    let N = arr.length;
    numberOfPasses(arr, N);

    // This code is contributed by rakeshsahni

</script>
```

**Output**

```
2 3 3 2 1 3 
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*