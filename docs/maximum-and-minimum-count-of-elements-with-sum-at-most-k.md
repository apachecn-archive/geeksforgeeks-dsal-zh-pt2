# 和最多为 K 的元素的最大和最小计数

> 原文:[https://www . geesforgeks . org/最多 k 个元素的最大和最小计数/](https://www.geeksforgeeks.org/maximum-and-minimum-count-of-elements-with-sum-at-most-k/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)**arr【】**和一个整数 **K** ，任务是找到**最大**和**最小**个元素，其[和](https://www.geeksforgeeks.org/sum-function-python/)之和小于或等于 **K** 。

**示例:**

> **输入:** N = 4，arr[ ] = {6，2，1，3}，K = 7
> **输出:** 3 1
> **说明:**
> 和小于等于 K 的元素最大个数为 3 即【1，2，3】
> 和小于等于 K 的元素最小个数为 1 即【6】
> 
> **输入:** N = 5，arr[] = {6，2，11，3，20}，K = 50
> **输出:** 5 5

**方法:**这个问题可以通过[对数组 arr[]进行排序来解决。](https://www.geeksforgeeks.org/arrays-sort-in-java-with-examples/)按照以下步骤解决这个问题:

*   [对数组 arr[]进行排序。](https://www.geeksforgeeks.org/sort-array-wave-form-2/)
*   将变量 **maxNumEle** 和 **minNumEle** 初始化为 **0** ，以存储元素的最小和最大数量，其和小于或等于 **K** 。
*   初始化一个变量 **cumSum1** 来存储数组 **arr[]的累计和。**
*   [使用变量 **i:** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**中迭代
    *   在 **cumSum1** 中添加电流元素。
    *   如果**累计 1** 小于等于 **K，**则在**最大值**中增加 **1** ，否则**断开**回路。
*   初始化一个变量 **cumSum2** 来存储数组**arr【】**的累计和。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【N-1，0】**中迭代:
    *   在 **cumSum2** 中添加电流元素。
    *   如果 **cumSum2** 小于等于 **K** ，则在 **minNumEle 中增加 **1** ，否则**断开回路。
*   完成以上步骤后，打印 **maxNumEle** 和 **minNumEle** 作为答案**。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;
// Function to find the maximum
// and minimum number of elements
// whose sum is less than equal
// to K
int findMinMax(int arr[], int N, int K)
{

    // Sorting both arrays
    sort(arr, arr + N);

    // To store the minimum and maximum
    // number of elements whose sum is
    // less than equal to K
    int maxNumEle = 0;
    int minNumEle = 0;

    // Store the cumulative sum
    int i, cumSum1 = 0;

    // Iterate in the range [0, N-1]
    for (i = 0; i < N; i++) {
        cumSum1 += arr[i];

        // If cumSum1 is less than K
        if (cumSum1 <= K)
            maxNumEle += 1;
        else
            break;
    }
    // Store the cumulative sum
    int cumSum2 = 0;

    // Iterate in the range [N-1, 0]
    for (i = N - 1; i >= 0; i--) {

        cumSum2 += arr[i];

        // If cumSum2 is less than K
        if (cumSum2 <= K)
            minNumEle += 1;
        else
            break;
    }
    // Print the value of maxNumEle and minNumEle
    cout << maxNumEle << " " << minNumEle;
}
// Driver Code

int main()
{
    // Given Input
    int N = 4;
    int K = 7;
    int arr[] = { 6, 2, 1, 3 };

    // Function Call
    findMinMax(arr, N, K);

    return 0;
}
// This code is contributed by Potta Lokesh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.lang.*;
import java.util.*;

class GFG{

// Function to find the maximum
// and minimum number of elements
// whose sum is less than equal
// to K
static void findMinMax(int arr[], int N, int K)
{

    // Sorting both arrays
    Arrays.sort(arr);

    // To store the minimum and maximum
    // number of elements whose sum is
    // less than equal to K
    int maxNumEle = 0;
    int minNumEle = 0;

    // Store the cumulative sum
    int i, cumSum1 = 0;

    // Iterate in the range [0, N-1]
    for(i = 0; i < N; i++)
    {
        cumSum1 += arr[i];

        // If cumSum1 is less than K
        if (cumSum1 <= K)
            maxNumEle += 1;
        else
            break;
    }

    // Store the cumulative sum
    int cumSum2 = 0;

    // Iterate in the range [N-1, 0]
    for(i = N - 1; i >= 0; i--)
    {
        cumSum2 += arr[i];

        // If cumSum2 is less than K
        if (cumSum2 <= K)
            minNumEle += 1;
        else
            break;
    }

    // Print the value of maxNumEle and minNumEle
    System.out.println(maxNumEle + " " + minNumEle);
}

// Driver code
public static void main(String[] args)
{

    // Given Input
    int N = 4;
    int K = 7;
    int arr[] = { 6, 2, 1, 3 };

    // Function Call
    findMinMax(arr, N, K);
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the maximum
# and minimum number of elements
# whose sum is less than equal
# to K
def findMinMax(arr, N, K):

    # Sorting both arrays
    arr.sort()

    # To store the minimum and maximum
    # number of elements whose sum is
    # less than equal to K
    maxNumEle = minNumEle = 0

    # Store the cumulative sum
    cumSum1 = 0

    # Iterate in the range [0, N-1]
    for i in range(N):
        cumSum1 += arr[i]

        # If cumSum1 is less than K
        if cumSum1 <= K:
            maxNumEle += 1
        else:
            break

    # Store the cumulative sum
    cumSum2 = 0

    # Iterate in the range [N-1, 0]
    for i in range(N-1, 0, -1):

        cumSum2 += arr[i]

        # If cumSum2 is less than K
        if cumSum2 <= K:
            minNumEle += 1
        else:
            break

    # Print the value of maxNumEle and minNumEle
    print(maxNumEle, minNumEle)

# Driver Code
if __name__ == '__main__':

    # Given Input
    N = 4
    K = 7
    arr = [ 6, 2, 1, 3 ]

    # Function Call
    findMinMax(arr, N, K)
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the maximum
// and minimum number of elements
// whose sum is less than equal
// to K
static void findMinMax(int[] arr, int N, int K)
{

    // Sorting both arrays
    Array.Sort(arr);

    // To store the minimum and maximum
    // number of elements whose sum is
    // less than equal to K
    int maxNumEle = 0;
    int minNumEle = 0;

    // Store the cumulative sum
    int i, cumSum1 = 0;

    // Iterate in the range [0, N-1]
    for(i = 0; i < N; i++)
    {
        cumSum1 += arr[i];

        // If cumSum1 is less than K
        if (cumSum1 <= K)
            maxNumEle += 1;
        else
            break;
    }

    // Store the cumulative sum
    int cumSum2 = 0;

    // Iterate in the range [N-1, 0]
    for(i = N - 1; i >= 0; i--)
    {
        cumSum2 += arr[i];

        // If cumSum2 is less than K
        if (cumSum2 <= K)
            minNumEle += 1;
        else
            break;
    }

    // Print the value of maxNumEle and minNumEle
    Console.WriteLine(maxNumEle + " " + minNumEle);
}

// Driver code
static public void Main()
{

    // Given Input
    int N = 4;
    int K = 7;
    int[] arr = { 6, 2, 1, 3 };

    // Function Call
    findMinMax(arr, N, K);
}
}

// This code is contributed by target_2
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the maximum
// and minimum number of elements
// whose sum is less than equal
// to K
function findMinMax(arr, N, K) {
  // Sorting both arrays
  arr.sort();

  // To store the minimum and maximum
  // number of elements whose sum is
  // less than equal to K
  let maxNumEle = 0;
  let minNumEle = 0;

  // Store the cumulative sum
  let i,
    cumSum1 = 0;

  // Iterate in the range [0, N-1]
  for (i = 0; i < N; i++) {
    cumSum1 += arr[i];

    // If cumSum1 is less than K
    if (cumSum1 <= K) maxNumEle += 1;
    else break;
  }
  // Store the cumulative sum
  let cumSum2 = 0;

  // Iterate in the range [N-1, 0]
  for (i = N - 1; i >= 0; i--) {
    cumSum2 += arr[i];

    // If cumSum2 is less than K
    if (cumSum2 <= K) minNumEle += 1;
    else break;
  }
  // Print the value of maxNumEle and minNumEle
  document.write(maxNumEle + " " + minNumEle);
}
// Driver Code

// Given Input
let N = 4;
let K = 7;
let arr = [6, 2, 1, 3];

// Function Call
findMinMax(arr, N, K);

// This code is contributed by gfgking

</script>
```

**Output**

```
3 1
```

***时间复杂度:** O(NlogN)*
***辅助空间:** O(N)*