# 最大化 L 长导线可覆盖的圆形建筑数量

> 原文:[https://www . geeksforgeeks . org/最大化可被 l 长度电线覆盖的圆形建筑数量/](https://www.geeksforgeeks.org/maximize-number-of-circular-buildings-that-can-be-covered-by-l-length-wire/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，代表圆形建筑的直径 **N** 和长度为 **L** 的直线。任务是找到电线在建筑物周围绕一圈可以覆盖的最大连续建筑物数量。

**注意:**每栋建筑之间的距离为 1 个单位长度，因此从一栋建筑到达下一栋建筑需要额外的 1 个单位长度。

**示例:**

> **输入:** arr[] = {4，1，6}，L = 24
> **输出:** 2
> **说明:**一轮建筑将需要**π* d**长度的导线，其中**π**为 **3.14159** ， **d** 为圆的**直径**。
> 第一栋建筑→ 12.566 所需电线长度，剩余电线→ 24-12.566=11.434 -1(到达下一栋建筑)=10.434
> 同样，第二栋建筑 3.141 所需电线长度，剩余电线→10.434-3.141 = 7.292-1 = 6.292
> 第三栋建筑 18.849，为>剩余电线即
> 
> **输入:** arr[] = {2，5，3，4}，L = 36
> T3】输出: 3

**进场:**思路是用[贪婪](https://www.geeksforgeeks.org/greedy-algorithms/)进场。按照以下步骤解决问题:

*   初始化变量 **curr_sum，start，curr_count，max_count** 计算当前元素之和，当前计数，当前[子阵](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的起始指数，以及覆盖建筑物的最大计数。
*   [在**【0，N-1】、**范围内遍历 **i** 的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)
    *   更新所需导线长度的当前总和， **curr_sum += arr[i] * 3.14**
    *   如果 [**i** 大于 0](https://www.geeksforgeeks.org/java-long-compareto-with-examples/) ，则将 **curr_sum** 增加 1。
    *   如果 **curr_sum ≤ L** 。将**当前计数**增加 1
    *   否则，从当前组中排除 **arr【开始】**
        *   更新**curr _ sum = curr _ sum –((双)arr[start] * 3.14)**
        *   将 **curr_sum** 减 1
        *   将**开始**指针增加 1
        *   将**电流计数**减 1
*   更新**最大计数**，即**最大计数=最大(当前计数，最大计数)。**
*   完成以上步骤后，打印 **max_count** 的值作为结果。

下面是上述方法的实现。

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
const double Pi = 3.141592;

// Function to find the maximum
// number of buildings covered
int MaxBuildingsCovered(int arr[], int N, int L)
{
    // Store the current sum
    double curr_sum = 0;

    int start = 0, curr_count = 0, max_count = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Add the length of wire required for
        // current building to cur_sum
        curr_sum = curr_sum + ((double)arr[i] * Pi);

        // Add extra unit distance 1
        if (i != 0)
            curr_sum += 1;

        // If curr_sum <= length of wire
        // increment count by 1
        if (curr_sum <= L) {
            curr_count++;
        }

        // If curr_sum > length of wire
        // increment start by 1 and
        // decrement count by 1 and
        // update the new curr_sum
        else if (curr_sum > L) {
            curr_sum = curr_sum - ((double)arr[start] * Pi);
            curr_sum -= 1;
            start++;
            curr_count--;
        }

        // Update the max_count
        max_count = max(curr_count, max_count);
    }

    // Return the max_count
    return max_count;
}

// Driver Code
int main()
{
    // Given Input
    int arr[] = { 4, 1, 6, 2 };
    int L = 24;

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << MaxBuildingsCovered(arr, N, L);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

static final double Pi = 3.141592;

// Function to find the maximum
// number of buildings covered
static int MaxBuildingsCovered(int arr[], int N,
                               int L)
{

    // Store the current sum
    double curr_sum = 0;

    int start = 0, curr_count = 0, max_count = 0;

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Add the length of wire required for
        // current building to cur_sum
        curr_sum = curr_sum + ((double)arr[i] * Pi);

        // Add extra unit distance 1
        if (i != 0)
            curr_sum += 1;

        // If curr_sum <= length of wire
        // increment count by 1
        if (curr_sum <= L)
        {
            curr_count++;
        }

        // If curr_sum > length of wire
        // increment start by 1 and
        // decrement count by 1 and
        // update the new curr_sum
        else if (curr_sum > L)
        {
            curr_sum = curr_sum - ((double)arr[start] * Pi);
            curr_sum -= 1;
            start++;
            curr_count--;
        }

        // Update the max_count
        max_count = Math.max(curr_count, max_count);
    }

    // Return the max_count
    return max_count;
}

// Driver Code
public static void main (String[] args)
{

    // Given Input
    int arr[] = { 4, 1, 6, 2 };
    int L = 24;

    // Size of the array
    int N = arr.length;

    // Function Call
    System.out.println(MaxBuildingsCovered(arr, N, L));
}
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python3 program for the above approach
Pi = 3.141592

# Function to find the maximum
# number of buildings covered
def MaxBuildingsCovered(arr, N,  L):
    # Store the current sum
    curr_sum = 0

    start = 0
    curr_count = 0
    max_count = 0

    # Traverse the array
    for i in range(N):
        # Add the length of wire required for
        # current building to cur_sum
        curr_sum = curr_sum + (arr[i] * Pi)

        # Add extra unit distance 1
        if (i != 0):
            curr_sum += 1

        # If curr_sum <= length of wire
        # increment count by 1
        if (curr_sum <= L):
            curr_count += 1

        # If curr_sum > length of wire
        # increment start by 1 and
        # decrement count by 1 and
        # update the new curr_sum
        elif(curr_sum > L):
            curr_sum = curr_sum - (arr[start] * Pi)
            curr_sum -= 1
            start += 1
            curr_count -= 1

        # Update the max_count
        max_count = max(curr_count, max_count)

    # Return the max_count
    return max_count

# Driver Code
if __name__ == '__main__':
    # Given Input
    arr = [4, 1, 6, 2]
    L = 24

    # Size of the array
    N = len(arr)

    # Function Call
    print(MaxBuildingsCovered(arr, N, L))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

static double Pi = 3.141592;

// Function to find the maximum
// number of buildings covered
static int MaxBuildingsCovered(int[] arr, int N,
                               int L)
{

    // Store the current sum
    double curr_sum = 0;

    int start = 0, curr_count = 0, max_count = 0;

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Add the length of wire required for
        // current building to cur_sum
        curr_sum = curr_sum + ((double)arr[i] * Pi);

        // Add extra unit distance 1
        if (i != 0)
            curr_sum += 1;

        // If curr_sum <= length of wire
        // increment count by 1
        if (curr_sum <= L)
        {
            curr_count++;
        }

        // If curr_sum > length of wire
        // increment start by 1 and
        // decrement count by 1 and
        // update the new curr_sum
        else if (curr_sum > L)
        {
            curr_sum = curr_sum - ((double)arr[start] * Pi);
            curr_sum -= 1;
            start++;
            curr_count--;
        }

        // Update the max_count
        max_count = Math.Max(curr_count, max_count);
    }

    // Return the max_count
    return max_count;
}

// Driver code
static void Main()
{

    // Given Input
    int[] arr = { 4, 1, 6, 2 };
    int L = 24;

    // Size of the array
    int N = arr.Length;

    // Function Call
    Console.Write(MaxBuildingsCovered(arr, N, L));
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach
      var Pi = 3.141592;

      // Function to find the maximum
      // number of buildings covered
      function MaxBuildingsCovered(arr, N, L) {
        // Store the current sum
        var curr_sum = 0;

        var start = 0,
          curr_count = 0,
          max_count = 0;

        // Traverse the array
        for (var i = 0; i < N; i++) {
          // Add the length of wire required for
          // current building to cur_sum
          curr_sum = curr_sum + parseFloat(arr[i]) * Pi;

          // Add extra unit distance 1
          if (i != 0) curr_sum += 1;

          // If curr_sum <= length of wire
          // increment count by 1
          if (curr_sum <= L) {
            curr_count++;
          }

          // If curr_sum > length of wire
          // increment start by 1 and
          // decrement count by 1 and
          // update the new curr_sum
          else if (curr_sum > L) {
            curr_sum = curr_sum - parseFloat(arr[start]) * Pi;
            curr_sum -= 1;
            start++;
            curr_count--;
          }

          // Update the max_count
          max_count = Math.max(curr_count, max_count);
        }

        // Return the max_count
        return max_count;
      }

      // Driver code
      // Given Input
      var arr = [4, 1, 6, 2];
      var L = 24;

      // Size of the array
      var N = arr.length;

      // Function Call
      document.write(MaxBuildingsCovered(arr, N, L));

      // This code is contributed by rdtank.
    </script>
```

**Output**

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)