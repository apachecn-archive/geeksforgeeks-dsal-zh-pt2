# 通过移除单个阵列元素

来尽可能减小相邻元素之间的最大差异

> 原文:[https://www . geeksforgeeks . org/通过移除单个数组元素来最小化相邻元素之间的最大差异/](https://www.geeksforgeeks.org/minimize-maximum-difference-between-adjacent-elements-possible-by-removing-a-single-array-element/)

给定一个由 **N** 个元素组成的[排序数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找出通过移除任何单个数组元素获得的所有数组的相邻元素之间的所有最大差异的最小值。

**示例:**

> **输入:** arr[ ] = { 1，3，7，8}
> **输出:** 5
> **解释:**
> 移除单个元素后所有可能的数组如下:
> **{3，7，8}:** 相邻元素之间的差异为{ 4，1}。最大值= 4。
> **{ 1，7，8}:** 相邻元素的区别是{ 6，1}。最大值= 6。
> **{ 1，3，8}:** 相邻元素之差为{ 2，5}。最大值= 5。
> 最后，(4，6，5)的最小值为 4，为所需输出。
> 
> **输入:** arr[ ] = { 1，2，3，4，5}
> **输出:** 1
> **解释:**
> 移除单个元素后所有可能的数组如下:
> { 2，3，4，5}:相邻元素之间的差异为{ 1，1，1}。最大值= 1。
> { 1，3，4，5}:相邻元素之间的差异为{ 2，1，1}。最大值= 2。
> { 1，2，4，5}:相邻元素之间的差异为{ 1，2，1}。最大值= 2。
> { 1，2，3，5}:相邻元素之间的差异为{ 1，1，2}。最大值= 2。
> 最后，(1，2，2，2)的最小值为 1，为所需输出。

**方法:**按照步骤解决问题

*   声明一个变量**MinValue =**[**INT _ MAX**](https://www.geeksforgeeks.org/int_max-int_min-cc-applications/)**来存储最终答案。**
*   **[遍历数组](https://www.geeksforgeeks.org/iterating-arrays-java/)，对于范围**【0，N–1】**内的 **i**

    *   声明一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **new_arr** ，它是除元素**arr【I】**之外的 **arr[]** 的副本
    *   将 **new_arr** 的最大相邻差存储在变量 **diff** 中
    *   更新 **最小值 = 最小值（最小值，差异）**** 
*   **返回 **MinValue** 作为最终答案。**

**下面是上述方法的实现。**

## **C++**

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find maximum difference
// between adjacent array elements
int maxAdjacentDifference(vector<int> A)
{
    // Store the maximum difference
    int diff = 0;

// Traverse the array
    for (int i = 1; i < (int)A.size(); i++) {

        // Update maximum difference
        diff = max(diff, A[i] - A[i - 1]);
    }

    return diff;
}

// Function to calculate the minimum
// of maximum difference between
// adjacent array elements possible
// by removing a single array element
int MinimumValue(int arr[], int N)
{
    // Stores the required minimum
    int MinValue = INT_MAX;

    for (int i = 0; i < N; i++) {

        // Stores the updated array
        vector<int> new_arr;

        for (int j = 0; j < N; j++) {

            // Skip the i-th element
            if (i == j)
                continue;

            new_arr.push_back(arr[j]);
        }

        // Update MinValue
        MinValue
            = min(MinValue,
                  maxAdjacentDifference(new_arr));
    }

    // return MinValue
    return MinValue;
}

// Driver Code
int main()
{
    int arr[] = { 1, 3, 7, 8 };
    int N = sizeof(arr) / sizeof(int);
    cout << MinimumValue(arr, N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;

class GFG
{

// Function to find maximum difference
// between adjacent array elements
static int maxAdjacentDifference(ArrayList<Integer> A)
{

    // Store the maximum difference
    int diff = 0;

// Traverse the array
    for (int i = 1; i < (int)A.size(); i++)
    {

        // Update maximum difference
        diff = Math.max(diff, A.get(i) - A.get(i - 1));
    }

    return diff;
}

// Function to calculate the minimum
// of maximum difference between
// adjacent array elements possible
// by removing a single array element
static int MinimumValue(int arr[], int N)
{

    // Stores the required minimum
    int MinValue = Integer.MAX_VALUE;

    for (int i = 0; i < N; i++) {

        // Stores the updated array
        ArrayList<Integer> new_arr=new ArrayList<>();

        for (int j = 0; j < N; j++) {

            // Skip the i-th element
            if (i == j)
                continue;

            new_arr.add(arr[j]);
        }

        // Update MinValue
        MinValue
            = Math.min(MinValue,
                  maxAdjacentDifference(new_arr));
    }

    // return MinValue
    return MinValue;

}

  // Driver code
    public static void main (String[] args) {
     int arr[] = { 1, 3, 7, 8 };
    int N = arr.length;
   System.out.print(MinimumValue(arr, N));

    }
}

// This code is contributed by offbeat
```

## **蟒蛇 3**

```
# Python3 program to implement
# the above approach
import sys

# Function to find maximum difference
# between adjacent array elements
def maxAdjacentDifference(A):

    # Store the maximum difference
    diff = 0

    # Traverse the array
    for i in range(1, len(A), 1):

        # Update maximum difference
        diff = max(diff, A[i] - A[i - 1])

    return diff

# Function to calculate the minimum
# of maximum difference between
# adjacent array elements possible
# by removing a single array element
def MinimumValue(arr, N):

    # Stores the required minimum
    MinValue = sys.maxsize

    for i in range(N):

        # Stores the updated array
        new_arr = []

        for j in range(N):

            # Skip the i-th element
            if (i == j):
                continue

            new_arr.append(arr[j])

        # Update MinValue
        MinValue = min(MinValue,
                       maxAdjacentDifference(new_arr))

    # return MinValue
    return MinValue

# Driver Code
if __name__ == '__main__':

    arr =  [ 1, 3, 7, 8 ]
    N = len(arr)

    print(MinimumValue(arr, N))

# This code is contributed by SURENDRA_GANGWAR
```

## **C#**

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find maximum difference
// between adjacent array elements
static int maxAdjacentDifference(List<int> A)
{

    // Store the maximum difference
    int diff = 0;

    // Traverse the array
    for(int i = 1; i < A.Count; i++)
    {

        // Update maximum difference
        diff = Math.Max(diff, A[i] - A[i - 1]);
    }
    return diff;
}

// Function to calculate the minimum
// of maximum difference between
// adjacent array elements possible
// by removing a single array element
static int MinimumValue(int[] arr, int N)
{

    // Stores the required minimum
    int MinValue = Int32.MaxValue;

    for(int i = 0; i < N; i++)
    {

        // Stores the updated array
        List<int> new_arr = new List<int>();

        for(int j = 0; j < N; j++)
        {

            // Skip the i-th element
            if (i == j)
                continue;

            new_arr.Add(arr[j]);
        }

        // Update MinValue
        MinValue = Math.Min(MinValue,
             maxAdjacentDifference(new_arr));
    }

    // Return MinValue
    return MinValue;
}

// Driver Code
public static void Main(string[] args)
{
    int[] arr = { 1, 3, 7, 8 };
    int N = arr.Length;

    Console.WriteLine(MinimumValue(arr, N));
}
}

// This code is contributed by ukasp
```

## **java 描述语言**

```
<script>

// JavaScript program to implement
// the above approach

// Function to find maximum difference
// between adjacent array elements
function maxAdjacentDifference(A)
{

    // Store the maximum difference
    let diff = 0;

// Traverse the array
    for (let i = 1; i < A.length; i++)
    {

        // Update maximum difference
        diff = Math.max(diff, A[i] - A[i-1]);
    }

    return diff;
}

// Function to calculate the minimum
// of maximum difference between
// adjacent array elements possible
// by removing a single array element
function MinimumValue(arr, N)
{

    // Stores the required minimum
    let MinValue = Number.MAX_VALUE;

    for (let i = 0; i < N; i++) {

        // Stores the updated array
        let new_arr=[];

        for (let j = 0; j < N; j++) {

            // Skip the i-th element
            if (i == j)
                continue;

            new_arr.push(arr[j]);
        }

        // Update MinValue
        MinValue
            = Math.min(MinValue,
                  maxAdjacentDifference(new_arr));
    }

    // return MinValue
    return MinValue;

}

// Driver code

    let arr = [ 1, 3, 7, 8 ];
    let N = arr.length;
   document.write(MinimumValue(arr, N));

</script>
```

****Output:** 

```
4
```** 

*****时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)***